# 📺 Paid Ads Report — RetroStyle Games

**Window:** May 1 → May 15, 2026 (2 weeks)
**Generated:** 2026-05-15

---

## 💰 Spend distribution

```mermaid
pie title Total Ad Spend $2,684 (2 weeks)
    "LinkedIn B2B"      : 1641
    "Google Product UAC" : 662
    "Meta Ads"          : 213
    "Google B2B Search" : 168
```

| Platform | Spend | Share | Active Campaigns |
|---|---:|---:|---:|
| 🟦 **LinkedIn B2B** | $1,641 | **61%** | 9 |
| 🟧 **Google Product (UAC)** | $662 | 25% | 2 |
| 🔵 **Meta Ads** | $213 | 8% | 1 |
| 🟩 **Google B2B (Search)** | $168 | 6% | 1 |
| **TOTAL** | **$2,684** | 100% | 13 |

---

## ⚡ Conversion reality check

```mermaid
%%{init: {'theme':'base', 'themeVariables': {'primaryColor':'#ff8c42'}}}%%
graph LR
    A[💵 $2,684 spend] --> B{Conversion tracked?}
    B -->|✅ Working| C[🟧 Google UAC<br/>5,842 conversions<br/>$0.11 per conv]
    B -->|❌ Broken| D[🟦 LinkedIn B2B<br/>0 attributed leads<br/>$1,641 dark spend]
    B -->|❌ Broken| E[🟩 Google B2B<br/>0 main conv<br/>$168 dark spend]
    B -->|⚠️ Undercount| F[🔵 Meta Pixel: 1<br/>Coda actual: 16<br/>15× discrepancy]
    style C fill:#90ee90
    style D fill:#ff6b6b
    style E fill:#ff6b6b
    style F fill:#ffd966
```

### Verdict

| Channel | $ spent | Tracked conv | Reality |
|---|---:|---:|---|
| 🟧 Last Pirate UAC | $452 | **5,241** ✅ | Truth — Firebase events firing clean |
| 🟧 Uncharted Tier 1 UAC (paused) | $210 | 601 ✅ | Truth — paused mid-window |
| 🟦 LinkedIn (9 campaigns) | $1,641 | 0 ❌ | UTM + Form submit + Insight Tag — 3 layers broken |
| 🔵 Meta B2B Slots | $213 | 1 vs 16 ⚠️ | Pixel undercounts 15× — Lead event not firing on submit |
| 🟩 Google Playable Ads Search | $168 | 0 ❌ | Same submit-fail bug + multi-LP fragmentation |

---

## 🟦 LinkedIn B2B — Campaign Performance

**Total: $1,641 / 0 attributed leads**

```mermaid
%%{init: {'theme':'base'}}%%
graph TB
    subgraph "Stylized Group ($770)"
        S1[Stylized_Character_4<br/>$388 / 0.80% CTR / $4.00 CPC ⭐]
        S2[Stylized_Props_2<br/>$382 / 0.62% CTR / $10.93 CPC]
    end
    subgraph "Casual Group ($800)"
        C1[Casual_Characters_3<br/>$344 / 0.30% CTR / $10.77 CPC]
        C2[Casual_UIUXIcons_2<br/>$254 / 0.43% CTR / $14.99 CPC ❌]
        C3[Casual_LiveOps_4<br/>$162 / 0.29% CTR / $8.08 CPC]
        C4[Casual_Match-3_4<br/>$24 / 0.32% CTR / $4.73 CPC]
        C5[Casual_Characters-Anim_1<br/>$16 / 0.27% CTR / $16.06 CPC ❌]
    end
    subgraph "Mixed Group ($70)"
        M1[Mixed_Trailers_2<br/>$61 / 0.30% CTR / $12.19 CPC]
        M2[Free-Assets_Indie<br/>$9 / 0.51% CTR / $4.29 CPC]
    end
    style S1 fill:#90ee90
    style C2 fill:#ff6b6b
    style C5 fill:#ff6b6b
```

### CPC efficiency leaderboard

```
$/Click (lower = better)

Stylized_Character_4     ████░░░░░░░░░░░░░░░░░░  $4.00  ⭐ BEST
Free-Assets_Indie        ████░░░░░░░░░░░░░░░░░░  $4.29
Casual_Match-3_4         █████░░░░░░░░░░░░░░░░░  $4.73
Casual_LiveOps_4         ████████░░░░░░░░░░░░░░  $8.08
Casual_Characters_3      ██████████░░░░░░░░░░░░  $10.77
Stylized_Props_2         ██████████░░░░░░░░░░░░  $10.93
Mixed_Trailers_2         ████████████░░░░░░░░░░  $12.19
Casual_UIUXIcons_2       ███████████████░░░░░░░  $14.99  ❌ WORST
Casual_Characters-Anim_1 ████████████████░░░░░░  $16.06  ❌ WORST
```

### 🏆 Top concept: **Stylized 3D Characters & Props**
Best CTR (0.80%) + cheapest CPC ($4.00). Production benchmark.

### 🔻 Bottom concepts: **Casual UI/UX + Animation**
$15-16 per click for 0.27-0.43% CTR. Either creative refresh or cut.

### 🚨 Why 0 attributed leads (3 broken layers)

```mermaid
flowchart TD
    A[LinkedIn Ad Click] -->|user lands| B[Landing Page]
    B -->|user fills form| C{Submit fires<br/>conversion event?}
    C -->|❌ Bug 1: form silent fail| X1[Lead lost<br/>no Pixel event]
    C -->|✅ but| D{UTM tags<br/>propagated?}
    D -->|❌ Bug 2: utm_medium missing<br/>0/188 campaigns| X2[GA4 channel = 'Unassigned'<br/>not 'Paid Social']
    D -->|✅ but| E{LinkedIn Insight Tag<br/>firing?}
    E -->|❌ Bug 3: tag via dead Elementor snippet| X3[No back-attribution<br/>to LinkedIn]
    E -->|✅| F[✅ Conversion counted]
    style X1 fill:#ff6b6b
    style X2 fill:#ff6b6b
    style X3 fill:#ff6b6b
```

---

## 🟧 Google Ads — Product (UAC) — The Working Engine

**Total: $662 / 5,842 attributed conversions / $0.11 per conv**

| Campaign | Status | Spend | Imp | Clicks | Conv | All Conv |
|---|---|---:|---:|---:|---:|---:|
| 🚀 30.03.2026 LP - in-app | ✅ ENABLED | $452 | 182,459 | 8,271 | **5,241** | 24,619 |
| ⏸ Uncharted Island 23/04 Tier 1 | PAUSED | $210 | 51,220 | 1,707 | 601 | 3,083 |

```mermaid
%%{init: {'theme':'base'}}%%
graph LR
    A[💵 $452] -->|spend| B[8,271 clicks]
    B --> C[5,241 main conversions]
    C --> D[💎 $0.086 per conv]
    style D fill:#90ee90
```

🎯 **Last Pirate retention machine** — best-in-portfolio efficiency. **Don't touch what works.**

⏸ **Uncharted Tier 1 paused** — was tracking $0.35/conv (still great). Investigate pause reason — creative fatigue? Budget exhaustion? D7 ROAS dip?

---

## 🟩 Google Ads — B2B (Search keywords)

**Total: $168 / 0 main conversions**

| Campaign | Status | Spend | Imp | Clicks | **CTR** | Main Conv | All Conv |
|---|---|---:|---:|---:|---:|---:|---:|
| Playable Ads Search | ENABLED | $168 | 132 | 16 | **12.1%** 🚀 | **0** ❌ | 1 |

### Paradox: best CTR, worst conversion

**12.1% CTR** is **20× above LinkedIn average** (0.4%). Keywords match intent perfectly. People who search "playable ads services" click.

But:
- **0 main conversions** in 16 clicks
- Same site-side bugs as LinkedIn (form submit fail, UTM, conversion action mismatch)
- 4 different `/playable-ads*` landing page variants split attribution

**Projection:** at current rate, this campaign will burn ~$380 by end of May with 0 measurable leads. Q2 burn ~$1,500 if unchanged.

---

## 🔵 Meta Ads — Pixel vs Reality

**Total: $213 / 1 Pixel lead vs 16 Coda submissions**

| Campaign | Status | Spend | Imp | Clicks | CTR | CPC | Pixel Lead | Coda actual |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| B2B Slots – Advantage -08/05/2026 | ACTIVE | $213 | 33,329 | 837 | 2.51% | $0.25 | **1** | **16** |

```mermaid
pie title Coda submissions (16 total) from this Meta campaign
    "🇷🇴 Romania (junk gmails)" : 5
    "🇧🇬 Bulgaria (duplicates)" : 4
    "🇵🇱 Poland (same IP)" : 2
    "🇮🇹 Italy (typo email)" : 1
    "🇺🇸 USA (potentially real)" : 1
    "🇵🇹 Portugal (Interested)" : 1
    "Anonymized garbage" : 2
```

### 🚨 Quality signals

| Signal | Detail |
|---|---|
| Emails | `21312312@gmail.com`, `1233123@gdsadfa.com`, `edigile8641@magilc.om` (typo) |
| Duplicates | `vasilecatalinanicoleta21@gmail.com` submitted **3× in one day** |
| Geo | 11 of 16 from low-purchasing-power Eastern Europe |
| Pipedrive match | 0 of 14 anonymized leads → no Lead Status assigned |

### 🎯 What's happening

```mermaid
flowchart LR
    A[Meta optimization] -->|trains on| B[1 Pixel lead]
    B -->|finds 'similar'| C[Eastern Europe<br/>incentive farms]
    C -->|leads| D[Coda fills with junk]
    D -->|but Pixel<br/>can't see| B
    style B fill:#ffd966
    style C fill:#ff6b6b
    style D fill:#ff6b6b
```

Pixel sees 1 lead → trains on that profile → finds similar audiences in low-cost geo → generates more form-fills → submit fails Pixel detection → loop continues with bad signal.

**Cost per junk lead: $15.20.** Cost per real lead: ~$107 (likely 2 of 16 = Portugal + US).

---

## 🧩 Cross-platform insights

### The big picture

```mermaid
%%{init: {'theme':'base'}}%%
graph TD
    BUDGET[💰 $2,684 spent] --> WORKING[$662 working<br/>Google Product UAC]
    BUDGET --> DARK[$1,981 dark spend<br/>LinkedIn + Google B2B + Meta]
    WORKING --> RESULT1[5,842 attributed<br/>installs/in-app conv ✅]
    DARK --> RESULT2[~5-10 real B2B leads<br/>none attributable to platform ❌]
    style WORKING fill:#90ee90
    style DARK fill:#ff6b6b
    style RESULT1 fill:#90ee90
    style RESULT2 fill:#ff6b6b
```

### Root cause: 3 site-side bugs blocking all B2B attribution

| Bug | Impact | Where |
|---|---|---|
| 🐛 Form submit silently fails | Leads fill form, click submit, nothing happens | `/outsourcing/b2b-game-art/`, portfolio Interested modal — **structural across site** |
| 🐛 UTM tagging absent | LinkedIn ad clicks land without `utm_medium=cpc/paid_social` | 0 of 188 LinkedIn campaigns tagged |
| 🐛 LinkedIn Insight Tag broken | Dead Elementor snippet hosting it | GTM container audit (Session 7) |

Fix any ONE and the whole funnel starts to leak less. Fix all three and **$1,981/2-weeks dark spend becomes measurable.**

---

## 🎯 Action priorities

### Critical (this week)

1. **Fix form submit** silent fail (one fix unblocks ALL B2B channels simultaneously)
2. **UTM hygiene** — mass update 188 LinkedIn campaigns destination URLs via API
3. **Pause `slots_andromeda`** Meta campaign OR restrict to US/UK/DE only

### High (next 2 weeks)

4. Investigate Uncharted Tier 1 paused — restart if salvageable (was $0.35/conv)
5. LinkedIn budget reallocation — Stylized winners +50%, Casual UI/UX & Animation cut
6. Consolidate 4 `/playable-ads*` landing variants into one URL

### Strategic

7. Add company name + budget required field to forms — filter junk traffic
8. Set up Telegram-bot alerts for "0 conversions in 7 days" on any B2B campaign
9. A/B test Stylized concept on new geo (DACH? US tier1?)

---

## 📊 At-a-glance dashboard

```
Last 2 weeks (May 1-15, 2026)

  💵 Spend  ████████████████████████████████  $2,684
  🟦 LinkedIn   ███████████████████░░░░░░░░░░░  61%  ❌ 0 attributed
  🟧 Google UAC ████████░░░░░░░░░░░░░░░░░░░░░░  25%  ✅ 5,842 conv
  🔵 Meta       ███░░░░░░░░░░░░░░░░░░░░░░░░░░░   8%  ⚠️ 1 vs 16 mismatch
  🟩 Google B2B ██░░░░░░░░░░░░░░░░░░░░░░░░░░░░   6%  ❌ 0 main conv

  📈 Working:   $662 → 5,842 conv ($0.11/conv) ✅
  📉 Dark spend: $1,981 → 0-10 untracked leads ❌

  🐛 3 site bugs blocking attribution:
     1. Form submit silent fail
     2. UTM tags missing on ad URLs
     3. LinkedIn Insight Tag via dead snippet

  🎯 Highest leverage: Fix #1 — unblocks all 3 B2B channels at once.
```

---

*Data sources: LinkedIn Marketing API, Meta Graph API v25, Google Ads API v21, Coda Conversions cross-reference. Currency UAH→USD at 43.85 rate (exchangerate-api.com, May 11).*
