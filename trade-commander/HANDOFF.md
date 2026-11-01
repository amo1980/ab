# TRADE COMMANDER — handoff

Last updated 1 Nov 2026. Read this first in a new session, then paste `SYSTEM_PROMPT.md` as the opening message.

## 1. Where things stand

**Done**
- Prompt built through four rounds of edits: browser control of MRKT, portal AI as a cross-check, optional Jev classifier, trade-style selection from market history, dashboard with journal and review loop, annotated charts, collapsible ideas.
- Jev researched. Conclusion: use as a downgrade-only text checker, in shadow mode for the first 25 ideas; use the Jev classifier, not Jev Router.
- Stage 0 answers recorded (access, alerts, scan interval, timezone, Jev key held, dashboard as an artifact).
- Stage 1 Watchlist: done.
- Stage 2 Hard risk rules: done.
- Stage 5B Dashboard: built and live.
- Idea I-0001 logged: XAUUSD, NO TRADE (onboarding incomplete), with an annotated chart from the 30 Oct screenshot.

**Not done**
- No live browser session yet. Everything so far came from screenshots, so the Stage 0 feature map still has to be built by browsing.
- Stages 3, 3B, 4, 5 and 6.
- The dashboard's automatic check never returned a result after the second update. The first load showed every dataset loading except the empty trade journal, which was fixed by adding a "journal opened" row.

## 2. Next session: how to start

1. Open the **Claude desktop app** with **Claude in Chrome** or the **built-in browser** turned on. The cloud session used so far had no browser tool.
2. Log in to https://app.mrktedge.ai/ yourself in that browser.
3. Paste `SYSTEM_PROMPT.md` as the first message.
4. Store the OpenRouter key as an environment variable or secret (e.g. `OPENROUTER_API_KEY`). Never paste it into chat.
5. Ask Claude to finish Stage 0: browse every portal section, build the feature map, confirm the portal's time zone, and confirm which chart is the live confirmation chart.
6. Then answer the Stage 3 questions (section 4).
7. After CONFIRMED: start scanning with `/loop 5m` and turn on push notifications.

## 3. Open questions

| # | Question | Stage |
|---|---|---|
| 1 | Which time is the NY open: 08:00 New York (13:00 GMT from 2 Nov) or 09:30 (14:30 GMT)? Does the 12:00–16:00 GMT NY window need moving after the US clock change? | 2 |
| 2 | Is the portal chart (labelled "MRKT Charts") the TradingView chart for live confirmation? | 0 |
| 3 | Portal time zone (the calendar looked like UTC) | 0 |
| 4 | Portal AI usage limits | 0 |
| 5 | Fed rate shows 3.88% on the Economy page but 4.00% on Rates: which is meant? | 0 |
| 6 | Jev probability threshold (default 70%) and shadow sample size (default 25) | 0 |
| 7 | How old data can be before it's stale (minutes) | 0 |
| 8 | Pip values and contract sizes for the .s symbols, checked in MT5 | 5 |

## 4. Stage 3 questions (asked, not yet answered)
1. Upload or paste the trading plan and the Basemode / trading-101 material.
2. Name each setup and describe it (order block or fair value gap pullback, break of structure and retest, liquidity sweep and reversal, etc.).
3. HTF trend: which timeframe (H4 or D1) and how is it defined (swing structure, moving average, MRKT bias tag)?
4. Entry timeframe and confirmation (M5 or M15; candle close, rejection wick, smaller-timeframe break of structure).
5. NY-open liquidity sweep: which liquidity counts (Asian, London, previous day high/low, pre-news range) and what confirms the sweep?
6. Stop placement method, within the caps: 20 pips EURUSD/GBPUSD, ~30 GBPJPY, $6 gold.
7. Do MRKT's Smart Money Flows levels count as key levels, or only as confirmation?

Then Stage 3B (approved styles and per-style rules), Stage 4 (Magic Keys features and management rules: partials, break-even trigger and buffer, trailing, weekend and news closes), Stage 5 (MT5 server time, symbol specs), Stage 6 (summary, then CONFIRMED).

## 5. Things to remember
- **Minimum lot vs $2 risk.** At 0.01 lot: EURUSD/GBPUSD stops ≤ 20 pips (≈ $0.10/pip), GBPJPY ≤ ~30 pips, gold ≤ $6 at the 3% gold allowance. Most qualifying trades will be FX scalps or day trades.
- **Gold:** one loss uses 3% of the 5% daily limit, so block a second gold trade that day after a gold loss.
- **Bank of England decision on 5 Nov.** MRKT showed a 98% chance of a 25 bp hike. High impact for GBPUSD and GBPJPY.
- **US clocks changed on 1 Nov.** New York is now GMT−5.
- **Market snapshot (30 Oct, from screenshots):**
  - Fed 4.00%: hike 70% priced for 9 Dec
  - ECB 2.50%: hike 81% priced for 17 Dec
  - BoE 3.75%: hike 98% priced for 5 Nov
  - BoJ 1.25%: hike 78% priced for 18 Dec
  - US data: CPI 3.7%, core PCE 3.6%, PPI 6.3%, unemployment 4.2%, NFP 29.0K
  - Gold: H1 at 3877.61 (−1.56%); MRKT resistances 3973 and 3920, target 3850, bias tag "Bearish · Reversal Risk"

## 6. Dashboard artifact

- **Link:** https://claude.ai/artifact/W66oSf91xQgvW9v4KKfWyN (title "Trade Commander"). Private until shared from its Share menu.
- **Type:** the claude.ai **Dashboard** artifact type. The page and its data live in the artifact's own store, not in published files. Never publish `index.html` or a `file_path` to it.
- **Tools:** `ArtifactData` (load with ToolSearch) to read and write the store; `Artifact` with `asset: true` to upload data files.
- **Local copy** of the page and data: `trade-commander/dashboard/` in this repo. Edit these, then push them to the store as below.

### Store documents (versions as of handoff)
| Document | Version | What it is |
|---|---|---|
| `dash/meta` | 1 | `{title: "Trade Commander"}` |
| `files/index.html` | 4 | `{text: <page HTML>}`, built from `dashboard/index.html` |
| `datasets/ideas` | 2 | Idea log → `/_blob/eabcf7149c98411924534dde576d9853` (ideas.json) |
| `datasets/trades` | 2 | Trade journal → `/_blob/23c343cbc987717150d16ae14f87025f` (trades.json) |
| `datasets/rules` | 4 | Risk rules and settings → `/_blob/706edbe293dcf8577d24c99f8ee5e095` (rules.json) |
| `datasets/onboarding` | 5 | Stage progress → `/_blob/2d652516c2fc6735153f31e75aaf7e7c` (onboarding.json) |
| `datasets/rates` | 1 | Central banks snapshot → `/_blob/2416671e2c737e2ef3a97332f208fa53` (rates.json) |
| `datasets/usmacro` | 1 | US economy snapshot → `/_blob/592008b9546ae74858418618535db96f` (usmacro.json) |
| `datasets/reviews` | 1 | Review log → `/_blob/3fe12b77739415440d27ace34013b51b` (reviews.json) |

Versions change with every write. Read a document first if you're unsure of its version.

### How to update data
1. Edit the JSON file in `trade-commander/dashboard/data/`. Each file must be an array of row objects and **never empty** (an empty array fails to load).
2. Upload it: `Artifact` with `url` = the dashboard link, `asset: true`, `file_path` = the JSON file. One JSON file per call. Note the returned `/_blob/<id>`.
3. Point the dataset at it: `ArtifactData` `update` on `datasets/<id>` with `if_version`, setting `source: {kind: "file", url: "/_blob/<id>", name: "<file>.json"}` and `updated: {at: <ISO time>, by: "Claude"}`. Batch several updates in one call.
4. Optionally check `data/users/me` doc `check` (and `runs`) a few times; don't loop on it.

### How to update the page
Edit `dashboard/index.html`, wrap it as `{"text": <html>}` in a JSON file, then `ArtifactData` `set` on `files/index.html` with `if_version`. The page follows the Dashboard type's "one writer" rule:
- fixed text lives in the HTML;
- anything the data decides is a `data-draw` element filled by `dash.draw`;
- tables carry `data-source` and `data-row-key`, and each `<th>` a `data-field`.

### Row schemas
- **ideas:** `id` (I-0001…), `logged_utc`, `pair`, `direction`, `style`, `status` (GO / WAIT / STAND DOWN / NO TRADE / BLOCKED BY RISK RULE), `score` (number or null), `mrkt_evidence`, `reason`, `entry_zone`, `stop_loss`, `targets`, `risk`, `invalidation`, `portal_ai`, `jev`, `outcome` (what price did afterwards), `chart` (`data:image/jpeg;base64,…`). Shown as collapsible cards, newest first; GO and WAIT start open.
- **trades:** `id` (T-0001…), `kind` (`"trade"`, or `"note"` for the T-0000 "journal opened" row that keeps the file non-empty), `opened_utc`, `pair`, `direction`, `style`, `entry`, `stop`, `exit`, `result_r` (number; null while open), `followed_plan` (Y/N), `notes`. Headline figures and results-by-style count only `kind: "trade"` rows.
- **rules:** `rule`, `value`, `status` (Set / To confirm / Pending).
- **onboarding:** `stage`, `name`, `status` (Done / In progress / Next / To confirm / Not started). Exactly one stage should be "In progress"; the page header shows it.
- **rates:** `bank`, `rate_pct`, `next_decision`, `implied_bp`, `most_likely`.
- **usmacro:** `indicator`, `value`, `period`, `change`.
- **reviews:** `id` (R-0001…), `date`, `type` (Setup / Daily / Weekly / Monthly), `summary`.

### Page sections
1. Header with the current onboarding stage.
2. Five headline figures: ideas logged, trades taken, net R, win rate, expectancy.
3. Trade ideas (collapsible, with charts).
4. Trade journal and results by style.
5. Risk rules, and onboarding stages.
6. Market context: central banks and US economy.
7. Review log.

**Still to add:** a "what happened to ideas I didn't take" view, a risk tracker (open risk and daily/weekly loss vs limits) and a rule-break log. All three are in the prompt but not built yet.
