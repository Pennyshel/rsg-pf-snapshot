# Meet Recorder — гайд для старых юзеров OBSidian

Если у тебя уже стоит [OBSidian Python тул](https://github.com/Nikola-Tesla-38/OBSidian) и ты пишешь миты руками через OBS — здесь описано, как **добавить авто-запуск записи по Google Calendar** через Chrome-расширение Meet Recorder + автозапуск всего бутерброда при включении ПК.

После настройки:

```
[просыпаешься, включаешь ПК]
    ↓ через ~90 секунд после логина
[OBSidian + OBS + Chrome поднимаются сами в трей]
    ↓
[в твоём календаре стартует мит с Meet-ссылкой]
    ↓ за 30 сек до начала
[Chrome открывает Meet таб / переиспользует существующий, OBS пишет]
    ↓ ты выходишь из мита
[OBS останавливает запись → OBSidian транскрибит → Make.com → vault → Discord саммари]
```

Ручных действий — ноль.

---

## TL;DR что надо сделать

1. Создать свой OAuth-клиент в Google Cloud Console (~5 минут)
2. Прописать `client_id` в `manifest.json` расширения
3. Загрузить расширение в Chrome как unpacked
4. Включить WebSocket-сервер в OBS, прописать URL+пароль в popup расширения
5. Залогиниться в Chrome через popup расширения
6. (Опционально, но рекомендуется) Настроить автозапуск через Планировщик заданий

---

## Шаг 1. Google Cloud Console — OAuth-клиент

Нужно один раз. Делается под тем аккаунтом, чей календарь будешь читать.

### 1.1 Создать проект

1. Открой [console.cloud.google.com](https://console.cloud.google.com/)
2. Сверху в селекторе проектов → **New Project**
3. Name: `meet-recorder` (или как тебе удобно)
4. **Create**, подожди 10 секунд, переключись на новый проект в селекторе

### 1.2 Включить Calendar API

1. Левое меню → **APIs & Services → Library**
2. В поиске: `Google Calendar API` → открыть карточку → **Enable**

### 1.3 OAuth consent screen

1. **APIs & Services → OAuth consent screen**
2. User Type:
   - **Internal** — если у тебя Workspace-аккаунт (`@retrostylegames.com` и т.п.) и **читать будешь только свой календарь из этого Workspace**. Это проще: не надо добавлять test users, нет лимитов, не нужна верификация Google
   - **External** — если личный gmail-аккаунт или нужно читать календари вне Workspace. Придётся добавлять себя в test users
3. Поля:
   - App name: `Meet Recorder`
   - User support email + Developer contact: твой email
   - Остальное по дефолту → **Save and Continue**
4. **Scopes** → **Add or Remove Scopes** → в поиске `calendar.events.readonly` → отметить `.../auth/calendar.events.readonly` → **Update** → **Save and Continue**
5. Если **External** — добавь себя в **Test users**
6. **Back to Dashboard**. **НЕ нажимай Publish App** — оставь в Testing-режиме, этого хватит

### 1.4 OAuth Client ID

1. **APIs & Services → Credentials**
2. **+ Create Credentials → OAuth client ID**
3. Application type: **Web application** *(именно она, не "Chrome Extension" — наш код использует `chrome.identity.launchWebAuthFlow`, а это Web app flow)*
4. Name: `Meet Recorder Dev` (что угодно)
5. **Authorized redirect URIs → + Add URI** → впиши:
   ```
   https://<ТВОЙ-EXTENSION-ID>.chromiumapp.org/
   ```
   Где `<ТВОЙ-EXTENSION-ID>` — длинная строка вида `cjhfagldgobpkklffnldccnlookfnjlk`. Этот ID задаётся `key`-полем в `manifest.json` расширения и **зашит в коде**. Открой `manifest.json` → найди `"key": "MII...."` → этот ключ через хэширование превращается в стабильный ID. Спроси у того кто дал тебе расширение — у него ID готовый
6. **Create** → откроется модалка с **Client ID** (что-то вроде `123456789-xxxxx.apps.googleusercontent.com`) → копируешь
7. **Client Secret игнорируешь** — он нам не нужен, наш flow его не использует

---

## Шаг 2. Прописать client_id в manifest.json

Открой `manifest.json` в папке с расширением, найди блок:

```json
"oauth2": {
  "client_id": "YOUR_OAUTH_CLIENT_ID_HERE.apps.googleusercontent.com",
  "scopes": [
    "https://www.googleapis.com/auth/calendar.events.readonly"
  ]
}
```

Замени `YOUR_OAUTH_CLIENT_ID_HERE.apps.googleusercontent.com` на свой Client ID из шага 1.4. Сохрани.

---

## Шаг 3. Загрузить расширение в Chrome

1. Открой `chrome://extensions`
2. Правый верх — включи **Developer mode**
3. Кнопка **Load unpacked** → выбери папку с расширением (где `manifest.json`)
4. Появится карточка "Meet Recorder" → запомни ID на ней. Он должен совпасть с тем, что ты прописал в redirect URI на шаге 1.4. Если **не совпадает** — значит `key` в manifest не сработал, надо разобраться (либо обновить redirect URI под фактический ID, либо запросить правильный `key` у того кто давал расширение)

---

## Шаг 4. OBS WebSocket

1. OBS Studio → **Tools → WebSocket Server Settings**
2. ✅ **Enable WebSocket server**
3. Порт: `4455` (дефолт, не меняй — manifest.json завязан на 4455)
4. Пароль: можешь поставить или оставить пустым. Если ставишь — нажми **Show Connect Info**, скопируй пароль
5. Apply / OK
6. Settings → Output → **Recording Path** должен указывать на ту же папку, которую слушает OBSidian Python (например `<OBSidian install dir>/video/`)
7. Recording Format — **mp4** или **hybrid mp4**

---

## Шаг 5. Sign in

1. Кликни на иконку Meet Recorder в Chrome-тулбаре → откроется popup
2. **OBS URL**: `ws://localhost:4455` (именно `localhost`, не IP, даже если OBS показывает 192.168.x.x — это для удалённых клиентов, мы локальные)
3. **OBS Password**: вставь, если ставил на шаге 4.4
4. **Save** → **Test connection** → должно вернуться "Connected" или "OK"
5. **Sign in with Google** → выбери нужный аккаунт. Если увидишь экран **"Google hasn't verified this app"** → нажми **Advanced → Go to Meet Recorder (unsafe)**. Для Testing-режима это нормально
6. Дай разрешение на чтение календаря

Готово. Расширение начинает поллить календарь раз в минуту.

---

## Шаг 6. Автозапуск через Планировщик заданий

Без этого после ребута всё стоит — нужно руками поднимать OBSidian/OBS/Chrome. Чтоб не парить мозг, лучше один раз настроить три задачи: OBSidian, OBS, Chrome.

### Вариант A — через PowerShell (быстро)

Открой PowerShell (необязательно администратора), **подставь свои пути** в первые три строки и выполни:

```powershell
# ── ПОДСТАВЬ СВОИ ПУТИ ──
$OBSidianStartBat = 'C:\Users\YOURNAME\OneDrive\Desktop\OBSidian-Nicolas\start.bat'
$OBSExe           = 'C:\Program Files\obs-studio\bin\64bit\obs64.exe'
$ChromeExe        = 'C:\Program Files\Google\Chrome\Application\chrome.exe'
# ─────────────────────────

$user = "$env:USERDOMAIN\$env:USERNAME"

# OBSidian (logon + 30s)
$action = New-ScheduledTaskAction -Execute $OBSidianStartBat -WorkingDirectory (Split-Path $OBSidianStartBat)
$trigger = New-ScheduledTaskTrigger -AtLogOn -User $user
$trigger.Delay = 'PT30S'
$settings = New-ScheduledTaskSettingsSet -AllowStartIfOnBatteries -DontStopIfGoingOnBatteries -RestartCount 3 -RestartInterval (New-TimeSpan -Minutes 1)
$principal = New-ScheduledTaskPrincipal -UserId $user -LogonType Interactive
Register-ScheduledTask -TaskName 'OBSidian Autostart' -Action $action -Trigger $trigger -Settings $settings -Principal $principal -Force | Out-Null

# OBS Studio (logon + 60s)
$action = New-ScheduledTaskAction -Execute $OBSExe -Argument '--disable-shutdown-check --minimize-to-tray' -WorkingDirectory (Split-Path $OBSExe)
$trigger = New-ScheduledTaskTrigger -AtLogOn -User $user
$trigger.Delay = 'PT1M'
Register-ScheduledTask -TaskName 'OBS Studio Autostart' -Action $action -Trigger $trigger -Settings $settings -Principal $principal -Force | Out-Null

# Chrome background (logon + 90s)
$action = New-ScheduledTaskAction -Execute $ChromeExe -Argument '--no-startup-window' -WorkingDirectory (Split-Path $ChromeExe)
$trigger = New-ScheduledTaskTrigger -AtLogOn -User $user
$trigger.Delay = 'PT1M30S'
Register-ScheduledTask -TaskName 'Chrome Background Autostart' -Action $action -Trigger $trigger -Settings $settings -Principal $principal -Force | Out-Null

Get-ScheduledTask | Where-Object { $_.TaskName -in @('OBSidian Autostart','OBS Studio Autostart','Chrome Background Autostart') } | Format-Table TaskName, State
```

После выполнения увидишь три задачи в `State: Ready`. Проверить руками: правый клик на задаче в `taskschd.msc` → **Run**.

### Дополнительно для Chrome

Открой [chrome://settings/system](chrome://settings/system) → включи **"Continue running background apps when Google Chrome is closed"**. Без этого `--no-startup-window` бесполезен — Chrome сразу схлопнется.

Если такой галки нет (Google её постепенно убирает) — убери `--no-startup-window` из аргументов задачи Chrome, тогда при логине будет открываться окно. Менее изящно, но работает.

### Вариант B — через GUI Планировщика

`Win + R` → `taskschd.msc` → **Создать задачу** для каждой из трёх. Триггер: при входе пользователя, отложить на 30/60/90 секунд. Действие: запуск exe с соответствующими аргументами. Подробности по полям — в [инструкции от Microsoft](https://learn.microsoft.com/ru-ru/windows/win32/taskschd/task-scheduler-start-page).

---

## Известные ограничения текущей версии

- **Instant meetings не записываются**. Если жмёшь "New meeting" в Meet — это не calendar event, расширение про него не знает. Решается отдельным TODO (детектор активного мита в DOM или ручная кнопка "Record now")
- **Waiting room / knock-to-join**. Если хост должен approve-нуть тебя, запись стартанёт сразу при клике Join, но мита ещё нет — в файле будут 30 секунд тишины
- **OAuth токен живёт 1 час**. После этого расширение молча перестанет работать с календарём, надо снова нажать **Sign in with Google** в popup'е. Auto-refresh — следующий TODO
- **Whitelist митов**. Сейчас записываются **ВСЕ** ивенты с Meet ссылкой. Если у тебя в календаре дантист и приватные миты — они тоже запишутся. На очереди: фильтр по организатору / тегу
- **Селекторы кнопки "Join"** могут сломаться если Meet поменяет UI. Сейчас content_script ловит `[jsname="Qx7uuf"]` и aria-label варианты на en/ru
- **Chrome должен быть запущен** (хотя бы в background-режиме) — service worker расширения живёт только пока Chrome жив

---

## Changelog

### 2026-05-11

- **Фикс**: расширение больше не открывает второй таб, если ты уже сам зашёл в Meet. Перед открытием проверяется `chrome.tabs.query` на существующий таб с тем же meeting ID — и переиспользуется
- **Фикс**: остановка записи теперь работает корректно. Раньше service worker фильтровал `meeting_ended` сигнал по `tabId`, и если ты был в своём ручном табе — сигнал игнорировался. Теперь принимается сигнал от **любого** таба с тем же meeting URL
- **Фикс**: end-of-call детектор переписан. Раньше ждал редиректа на `/landing` (~50 сек таймером Meet). Теперь дополнительно ловит DOM-маркеры — кнопку "Rejoin", "Return to home screen", текст "You left the meeting" (en + ru) — реагирует в течение ~2 секунд
- **Новое**: safety-net таймер. При старте записи ставится alarm на `event.end + 2 минуты`. Если все детекторы по какой-то причине промолчали — запись всё равно остановится сама
- **Новое**: auto-join теперь срабатывает **только** в табах, открытых расширением (через query-маркер `?meetrecorder=autojoin`). Если ты сам открыл Meet — content_script не будет авто-кликать Join за тебя
- **Новое**: автозапуск всего стека (OBSidian, OBS, Chrome) через Планировщик заданий — см. Шаг 6 выше
