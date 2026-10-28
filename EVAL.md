# Evaluation test set

Fill this in after every refresh, before you publish. The agent is the system under test.
You are the grader. Nothing here is automated on purpose: the point is to decide, with a
source you trust, whether the agent told you the truth.

**Ground truth sources.** Pick one and use the same one every time, so your scores are
comparable week to week:

- Prices: Google Finance (google.com/finance), Yahoo Finance, or your brokerage app.
- News: the article itself. Open the link. Check the date on the page.
- Calendar: the company's investor relations page (search "TICKER investor relations
  events"), or the Fed's own meeting calendar for FOMC dates.

Refresh date: 2026-10-28    Grader: number-checker agent
Refresh date (recheck): 2026-10-27 (BRIEF.asOf changed from 2026-10-28 to 2026-10-27 in the fix)    Grader: number-checker agent

## A. Prices (one row per ticker)

Pass if the dashboard's last price is within $0.10 of the ground truth for the same day
and the same price type (close vs intraday). If the agent recorded an intraday price,
compare against the intraday price at about the same time; do not compare it to a close.

| Ticker | Date shown | Price type shown | Dashboard price | Ground truth price | Source you used | Pass / Fail |
|---|---|---|---|---|---|---|
| NVDA | 2026-10-27 | close | 217.94 | 217.94 | Yahoo Finance history, https://finance.yahoo.com/quote/NVDA/history/ (Google Finance https://www.google.com/finance/quote/NVDA:NASDAQ returned "not supported on this device", so Yahoo used). Oct 21-26 closes 221.97 / 212.21 / 210.96 / 216.00 all match. | Pass |
| NVDA | 2026-10-28 11:51 AM ET | intraday | 217.26 | No 11:51 quote found. Yahoo at 12:11:26 PM EDT: 216.96; Oct 28 range so far 216.88 to 219.99, so 217.26 is inside Yahoo's range (but changelog says it is below stockanalysis's listed low 217.27). | https://finance.yahoo.com/quote/NVDA/history/ | Unconfirmed (not counted as Pass): no intraday quote at about 11:51 AM ET |
| JPM | 2026-10-27 | close | 335.79 | 335.79 | Yahoo Finance history, https://finance.yahoo.com/quote/JPM/history/ (Google Finance unavailable, see NVDA). Oct 21-26 closes 335.19 / 336.54 / 331.58 / 334.04 all match. | Pass |
| JPM | 2026-10-28 11:51 AM ET | intraday | 339.45 | No 11:51 quote found. Yahoo at 12:11:57 PM EDT: 339.70; Oct 28 range so far 335.18 to 339.81, so 339.45 is inside Yahoo's range (changelog says it is above stockanalysis's listed high 338.98). | https://finance.yahoo.com/quote/JPM/history/ | Unconfirmed (not counted as Pass): no intraday quote at about 11:51 AM ET |
| ACN | 2026-10-27 | close | 235.16 | 235.16 | Yahoo Finance history, https://finance.yahoo.com/quote/ACN/history/ (Google Finance unavailable). Oct 21-26 closes 240.26 / 258.74 / 249.37 / 247.23 all match. | Pass |
| ACN | 2026-10-28 11:51 AM ET | intraday | 245.45 | No 11:51 quote found. Yahoo at 12:11:25 PM EDT: 245.35; range 232.57 to 246.79. | https://finance.yahoo.com/quote/ACN/history/ | Unconfirmed (not counted as Pass) |
| COST | 2026-10-27 | close | 992.13 | 992.13 | Yahoo Finance history, https://finance.yahoo.com/quote/COST/history/ (Google Finance unavailable). Oct 21-26 closes 998.31 / 1018.21 / 1003.32 / 1005.16 all match. | Pass |
| COST | 2026-10-28 11:51 AM ET | intraday | 982.16 | No 11:51 quote found. Yahoo at 12:11:54 PM EDT: 983.56; range 980.32 to 984.73. | https://finance.yahoo.com/quote/COST/history/ | Unconfirmed (not counted as Pass) |
| LLY | 2026-10-27 | close | 1281.91 | 1281.91 | Yahoo Finance history, https://finance.yahoo.com/quote/LLY/history/ (Google Finance unavailable). Oct 21-26 closes 1270.75 / 1306.69 / 1273.46 / 1279.14 all match. | Pass |
| LLY | 2026-10-28 11:50 AM ET | intraday | 1294.17 | No 11:50 quote found. Yahoo at 12:11:53 PM EDT: 1291.22; range 1260.34 to 1299.43. | https://finance.yahoo.com/quote/LLY/history/ | Unconfirmed (not counted as Pass) |
| NVDA (recheck) | 2026-10-27 | close (latest: null) | 217.94 | 217.94 | Yahoo Finance history, re-opened 2026-10-28, https://finance.yahoo.com/quote/NVDA/history/ (Google Finance not used: unavailable on previous run). Oct 21-26 closes still match. | Pass |
| JPM (recheck) | 2026-10-27 | close (latest: null) | 335.79 | 335.79 | Yahoo Finance history, re-opened 2026-10-28, https://finance.yahoo.com/quote/JPM/history/. Oct 21-26 closes still match. | Pass |
| ACN (recheck) | 2026-10-27 | close (latest: null) | 235.16 | 235.16 | Yahoo Finance history, re-opened 2026-10-28, https://finance.yahoo.com/quote/ACN/history/. Oct 21-26 closes still match. | Pass |
| COST (recheck) | 2026-10-27 | close (latest: null) | 992.13 | 992.13 | Yahoo Finance history, re-opened 2026-10-28, https://finance.yahoo.com/quote/COST/history/. Oct 21-26 closes still match. | Pass |
| LLY (recheck) | 2026-10-27 | close (latest: null) | 1281.91 | 1281.91 | Yahoo Finance history, re-opened 2026-10-28, https://finance.yahoo.com/quote/LLY/history/. Oct 21-26 closes still match. | Pass |

Note: no earlier close (Oct 21 to Oct 26) failed for any ticker.

## B. Weekly change (one row per ticker)

The page computes this from the five closes. Pass if it is within 0.3 percentage points of
your own calculation: (last price minus the close five trading days earlier) divided by
that earlier close.

| Ticker | Dashboard weekly change | Your calculation | Pass / Fail |
|---|---|---|---|
| NVDA | -2.12% (Oct 21 close 221.97 to intraday 217.26) | -2.26% (Yahoo Oct 21 close 221.97 to Yahoo 12:11 PM quote 216.96); diff 0.14 pp. Close-to-close Oct 20 216.47 to Oct 27 217.94 would be +0.68%. Source: https://finance.yahoo.com/quote/NVDA/history/ | Pass (arithmetic and base close verified; end price is the unconfirmed intraday from A) |
| JPM | +1.27% (335.19 to 339.45) | +1.35% (335.19 to Yahoo 12:11 PM 339.70); diff 0.08 pp. Close-to-close Oct 20 335.26 to Oct 27 335.79: +0.16%. Source: https://finance.yahoo.com/quote/JPM/history/ | Pass (same caveat) |
| ACN | +2.16% (240.26 to 245.45) | +2.12% (240.26 to Yahoo 12:11 PM 245.35); diff 0.04 pp. Close-to-close Oct 20 239.12 to Oct 27 235.16: -1.66%. Source: https://finance.yahoo.com/quote/ACN/history/ | Pass (same caveat) |
| COST | -1.62% (998.31 to 982.16) | -1.48% (998.31 to Yahoo 12:11 PM 983.56); diff 0.14 pp. Close-to-close Oct 20 994.61 to Oct 27 992.13: -0.25%. Source: https://finance.yahoo.com/quote/COST/history/ | Pass (same caveat) |
| LLY | +1.84% (1270.75 to 1294.17) | +1.61% (1270.75 to Yahoo 12:11 PM 1291.22); diff 0.23 pp. Close-to-close Oct 20 1283.66 to Oct 27 1281.91: -0.14%. Source: https://finance.yahoo.com/quote/LLY/history/ | Pass (same caveat) |

| NVDA (recheck) | -1.82% (page: first to last of its five closes, Oct 21 221.97 to Oct 27 217.94) | +0.68% (Yahoo Oct 20 216.47 to Oct 27 217.94, five trading days earlier); diff 2.50 pp. Oct 21 to Oct 27 on Yahoo closes: -1.82%, diff 0.00 pp, but that is only four trading days. Source: https://finance.yahoo.com/quote/NVDA/history/ | Fail: window is 4 trading days, not 5. Correct value +0.68% |
| JPM (recheck) | +0.18% (335.19 to 335.79) | +0.16% (Yahoo Oct 20 335.26 to Oct 27 335.79); diff 0.02 pp. Oct 21 to Oct 27: +0.18%, diff 0.00. Source: https://finance.yahoo.com/quote/JPM/history/ | Pass (within 0.3 pp even on the 5-day definition) |
| ACN (recheck) | -2.12% (240.26 to 235.16) | -1.66% (Yahoo Oct 20 239.12 to Oct 27 235.16); diff 0.47 pp. Oct 21 to Oct 27: -2.12%, diff 0.00. Source: https://finance.yahoo.com/quote/ACN/history/ | Fail: correct value -1.66% |
| COST (recheck) | -0.62% (998.31 to 992.13) | -0.25% (Yahoo Oct 20 994.61 to Oct 27 992.13); diff 0.37 pp. Oct 21 to Oct 27: -0.62%, diff 0.00. Source: https://finance.yahoo.com/quote/COST/history/ | Fail: correct value -0.25% |
| LLY (recheck) | +0.88% (1270.75 to 1281.91) | -0.14% (Yahoo Oct 20 1283.66 to Oct 27 1281.91); diff 1.01 pp (and opposite sign). Oct 21 to Oct 27: +0.88%, diff 0.00. Source: https://finance.yahoo.com/quote/LLY/history/ | Fail: correct value -0.14% |

Recheck note: removing the Oct 28 intraday price shortened the page's window. `weekChange()` in index.html takes (last point minus first point) / first point, and with `latest` null the points are the five closes Oct 21 to Oct 27, which is four trading-day intervals. The check's definition is "the close five trading days earlier", which for Oct 27 is Oct 20. The page's arithmetic is correct for its inputs and every close is correct, so the Oct 21 to Oct 27 comparison the fix brief asked for matches exactly (0.00 pp on all five). On the five-trading-day definition, 4 of 5 fail. Inferred fix (for whoever edits BRIEF; not done here): add the Oct 20 close as a sixth entry in each `closes` list (NVDA 216.47, JPM 335.26, ACN 239.12, COST 994.61, LLY 1283.66, all Yahoo history) so the page's first-to-last spans five trading days.

Note: the page computes Oct 21 close to Oct 28 intraday (five trading days). The page's math is correct for its inputs and the Oct 21 base closes are verified, but the end price is about 20 minutes off the Yahoo quote used here, so B is only as good as the unconfirmed intraday prices in A.

## C. News grounding (one row per news item, three per ticker)

Open every link. Pass only if all four are true: the link opens, the headline matches the
article, the article date is within the last seven days, and the "why it matters" line is
supported by the article (not just plausible).

| Ticker | Headline (first few words) | Link opens | Headline matches | Dated within 7 days | "Why" is supported | Pass / Fail |
|---|---|---|---|---|---|---|
| NVDA | "NVIDIA and Oracle Expand NVIDIA Vera Rubin..." https://nvidianews.nvidia.com/news/nvidia-and-oracle-expand-nvidia-vera-rubin-to-multi-gigawatt-scale-and-bring-nvidia-vera-cpu-to-oracle-cloud-infrastructure | Yes | Yes | Yes (Oct 27, 2026) | Yes: "NVIDIA Vera Rubin NVL72 and NVIDIA Vera CPUs Are Now Generally Available on OCI." | Pass |
| NVDA | "NVIDIA and Meta to Expand Collaboration on Muse..." https://nvidianews.nvidia.com/news/nvidia-and-meta-to-expand-collaboration-on-muse-and-muse-family-of-models-amid-robust-growth | Yes | Yes | Yes (Oct 26, 2026) | Yes: "Meta intends to expand the deployment of NVIDIA infrastructure..." and "In addition, NVIDIA will invest $3 billion in Meta's equity offering." (the "links NVIDIA's money to its own demand" clause is the agent's own reading) | Pass |
| JPM | "Anthropic taps JPMorgan to lead IPO's U.S. retail sales..." https://www.investing.com/news/stock-market-news/anthropic-taps-jpmorgan-to-lead-ipos-us-retail-sales-bloomberg-reports-4977334 | Yes | Yes | Yes (Oct 27, 2026, 09:09 PM, no time zone) | No. Article supports the role: Anthropic "tapped JPMorgan Chase & Co (NYSE:JPM) to lead U.S. share sales to individual investors". It says nothing about underwriting fees or JPMorgan's wealth business; that part of the "why" is an inference. Secondhand (Investing.com citing Bloomberg). | Fail: "why" not supported (fees / wealth business) |
| JPM | "JPMorgan says ex-banker Rana pushed sister..." https://www.investing.com/news/stock-market-news/jpmorgan-says-exbanker-rana-pushed-sister-friend-to-lie-to-support-sexual-assault-case-4976447 | Yes | Yes | Yes (Oct 27, 2026) | Yes: "JPMorgan Chase urged a federal judge to dismiss a sexual harassment and discrimination lawsuit..." ("reputational more than financial" is the agent's framing) | Pass |
| JPM | "Jamie Dimon spent years warning..." https://fortune.com/2026/10/21/jamie-dimon-jpmorgan-china-critical-minerals-defense/ | Yes | Yes | Yes (Oct 21, 2026, exactly 7 days before asOf) | Yes: "it has financed or facilitated $230 billion into sectors it considers essential for economic and national security" ... "a year into its 10-year, $1.5 trillion Security and Resiliency Initiative." | Pass |
| ACN | "Accenture wins $151M Air Force ICBM..." https://www.investing.com/news/pro/accenture-wins-151m-air-force-icbm-engineering-contract-432SI-4977048 | Yes (headline only, "Pro News", subscriber sign-in prompt) | Yes (headline is the only content) | Yes (Oct 27, 2026, 05:19 PM) | No. There is no article body and no original source cited, so nothing supports the "adds to government backlog" line (the brief itself admits details are unconfirmed). | Fail: "why" unsupported, headline-only page |
| ACN | "Why is Accenture stock sliding today?" https://www.investing.com/news/stock-market-news/why-is-accenture-stock-sliding-today-93CH-4970187 | Yes | Yes | Yes (Oct 23, 2026) | Yes: "Shares of Accenture fell 4.6% in mid-day trading as a cluster of insider selling disclosures and a high-profile analyst downgrade combined..." and Baird downgraded "to Neutral from Outperform", arguing the "valuation fully reflecting — if not exceeding — the company's growth prospects." | Pass |
| COST | "Costco Remains a Defensive Compounder..." https://247wallst.com/investing/2026/10/27/costco-remains-a-defensive-compounder-awaiting-its-next-leg-up/ | Yes | Yes | Yes (Oct 27, 2026) | Yes: "Renewal rates reached 92.3% in the U.S. and Canada"; "free cash flow climbed 19.82% to $9.39 billion"; "trailing P/E of 48"; "At $1,005.16, Costco is a Hold." | Pass |
| LLY | "Lilly's retatrutide delivered greater A1C reduction..." https://www.prnewswire.com/news-releases/lillys-retatrutide-delivered-greater-a1c-reduction-and-more-than-double-the-weight-loss-of-ozempics-highest-approved-dose-in-head-to-head-trial-302921328.html | Yes | Yes | Yes (Oct 28, 2026) | Yes: "At 80 weeks, retatrutide met the primary and all key secondary endpoints, delivering greater A1C reduction..." vs Ozempic's highest approved dose (headline) | Pass |
| LLY | "Patrik Jonsson to retire after 36 years..." https://www.prnewswire.com/news-releases/patrik-jonsson-to-retire-after-36-years-ilya-yuffa-named-president-lilly-global-markets-302921191.html | Yes | Yes | Yes (Oct 27, 2026) | Yes: effective January 1, 2027, "Lilly's U.S. and international businesses will come together as Lilly Global Markets", led by Yuffa | Pass |
| LLY | "Lilly breaks ground in Richmond..." https://www.prnewswire.com/news-releases/lilly-breaks-ground-in-richmond-to-expand-american-manufacturing-of-next-generation-cancer-medicines-advancing-its-build-out-of-10-new-us-sites-since-2020-302916266.html | Yes | Yes | Yes (Oct 22, 2026) | Yes: "broke ground today on a new $5 billion manufacturing facility just west of Richmond, Virginia, in Goochland County" | Pass |

(Add rows as needed. Fifteen items is normal for five tickers.)

## D. Calendar (one row per event)

Pass if the event and its date appear on the source linked, and the date is in the future
relative to the refresh date.

| Ticker | Event | Date shown | Confirmed on source | Pass / Fail |
|---|---|---|---|---|
| JPM | FOMC rate decision (Oct 27-28 meeting) | 2026-10-28 | Yes. Fed calendar lists "October 27-28" for 2026, not marked tentative. Date equals asOf, so it is not before asOf. https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm | Pass |
| JPM | Quarterly dividend $1.65 payable (record Oct 6) | 2026-10-31 | Yes. JPMorganChase IR release (Sep 15, 2026): "a quarterly dividend of $1.65 per share", "payable on October 31, 2026", record "October 6, 2026". https://www.jpmorganchase.com/ir/news/2026/jpmc-declares-increased-common-stock-dividend-9-15 | Pass |
| COST | Dividend record date, $1.47 (payable Nov 13) | 2026-10-30 | Yes. Costco press release filed with SEC 8-K (Oct 14, 2026): "$1.47 per share", record "October 30, 2026", "payable November 13, 2026". Primary company source, though not the IR events page. https://www.sec.gov/Archives/edgar/data/0000909832/000090983226000096/costex9918-k101426.htm | Pass |
| LLY | Q3 2026 results; call 10 a.m. ET (confirmed) | 2026-10-29 | unconfirmed: could not open https://investor.lilly.com/events-and-presentations (HTTP 403). The brief's link is a Lilly press release reposted on Finviz (Oct 15, 2026), not the IR page; it reads "will announce its third-quarter 2026 financial results on October 29, 2026" and "The conference call will begin at 10 a.m. Eastern time." So the "confirmed" wording matches the company's own release. https://finviz.com/news/403165/lilly-confirms-date-and-conference-call-for-third-quarter-2026-financial-results-announcement | Fail (IR page could not be opened; likely Pass once a human checks it) |

## E. Omissions

Did the agent miss something a human analyst would have included? List anything you found
in the ground-truth sources that the brief does not mention (a big headline, an earnings
date inside the window). Each one counts as a Fail in the score below.

- 
- 

## F. Your own test cases

Write two tests of your own that none of the sections above cover. Examples students have
used: "the as-of date on the page matches the changelog date", "no ticker shows a flat
sparkline when the real stock moved", "the page still renders if I delete one ticker's
news list in the data". Write the test, run it, record the result.

| Test | How you checked | Pass / Fail |
|---|---|---|
| | | |
| | | |

## Score

| Section | Passes | Total | Rate |
|---|---|---|---|
| A. Prices | 5 | 10 | 50% (Oct 27 closes 5/5 Pass; Oct 28 intraday 0/5 confirmed) |
| B. Weekly change | 5 | 5 | 100% (end price inherits A's unconfirmed intraday) |
| C. News | 9 | 11 | 82% |
| D. Calendar | 3 | 4 | 75% |
| E. Omissions (fails only) | 0 | | |
| F. Your own | | | |
| **Overall** | | | |

Publish only if A and B are 100% and C is at least 80% after fixes. If a row failed, tell
Claude exactly which row and what the correct value is, let it fix only that, rerun the
`qa-reviewer` agent, and regrade that row. Keep the original Fail in this file: a record of
what the agent got wrong is more useful than a clean sheet.
