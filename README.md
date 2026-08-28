# Cash Flow Forecasting & Budgeting Model — NimbusFlow Technologies Inc.

A full FP&A cash flow forecasting and budgeting model built for a fictional B2B SaaS company, covering data cleaning, a 12-month rolling cash flow forecast, departmental budget vs. actual variance analysis, AR/AP aging, working capital, three-scenario forecasting, an executive KPI dashboard, and management reporting.

**File:** `NimbusFlow_Cash_Flow_Forecasting_Budgeting_Model.xlsx` — 12 linked sheets, 1,425 live formulas, zero calculation errors.

https://1drv.ms/x/c/1790eeaed48175a5/IQAnVcn9Xs1AT4MJZLMVL3KXAYTWnnngd_GRW5kJCE8Q3Uc?e=RSBTT5
---

## Demo Video



https://github.com/user-attachments/assets/50856e22-0ad2-4db3-a757-701f83d6f683



A walkthrough of the model — from raw data and assumptions, through the cash flow forecast and scenario analysis, to the executive dashboard.


<img width="968" height="833" alt="P5 (S3) in Outputs" src="https://github.com/user-attachments/assets/6989806e-b985-488f-a6e2-16d142b87995" />
<img width="1184" height="829" alt="P5 (S2) in Outputs" src="https://github.com/user-attachments/assets/bab3d6e5-668c-4008-8131-fcae716efc29" />
<img width="1471" height="783" alt="P5 (S1) in Outputs" src="https://github.com/user-attachments/assets/234e2cb3-7baf-4559-a1ae-d27d8947ee72" />

---

## Screenshots

| | |
|---|---|
| **Executive Dashboard** — KPI cards, trend charts, alert banners | ![Dashboard](./screenshots/dashboard.png) |
| **Cash Flow Forecast** — FY2026 actuals + FY2027 monthly forecast with liquidity tiers | ![Cash Flow](./screenshots/cash-flow-forecast.png) |
| **Budget vs. Actual** — department-level variance heatmap | ![Budget Variance](./screenshots/budget-variance-heatmap.png) |
| **Scenario Analysis** — Best / Base / Worst case comparison | ![Scenario Analysis](./screenshots/scenario-analysis.png) |
| **AR / AP Aging** — aging buckets, DSO/DPO, cash conversion cycle | ![AR AP Aging](./screenshots/ar-ap-aging.png) |
| **KPI Summary** — executive KPI matrix with formulas, targets, interpretation | ![KPI Summary](./screenshots/kpi-summary.png) |



---

## 1. Business Problem

Profitable-looking companies run out of cash all the time — revenue on the income statement doesn't mean cash in the bank, especially for a subscription business with annual billing, Net 30/45 customer terms, and lumpy CapEx. This project builds the tool an FP&A analyst would actually use to see that gap coming: a rolling cash forecast, a department-level budget to hold spend accountable, and an early-warning system for liquidity shortfalls — before they become a crisis for the executive team.

## 2. Company & Dataset

- **Company:** NimbusFlow Technologies Inc. — B2B SaaS project & workflow management software for SMBs, ~68% of revenue on upfront-billed annual contracts.
- **Fiscal Year modeled:** FY2026 actuals → FY2027 forecast.
- **Starting cash:** $850,000 · **Minimum cash reserve:** $300,000.
- **Dataset:** 180 transaction/budget records across 8 departments (Sales, Marketing, HR, Operations, IT, Admin, Finance, CapEx), 25 fields including Budget/Actual/Forecast amounts, cash inflow/outflow, AR/AP, and variance — cleaned per the data quality log in the `Data_Quality` tab (duplicate removal, date/currency standardization, department-name normalization, anomaly flagging).

## 3. Financial Model Architecture

| Tab | Purpose |
|---|---|
| `Assumptions` | Company profile, revenue/expense structure, payment terms, starting cash |
| `Raw_Data` | 180-row transaction dataset — single source of truth for every other tab |
| `Data_Quality` | Before/after cleaning log |
| `Budget` | Annual + monthly budget vs. actual by department, with a color-scaled variance heatmap |
| `Revenue_Forecast` | 12-month Base/Best/Worst revenue projection |
| `Expense_Forecast` | Fixed / Variable / Semi-Variable cost forecast |
| `Cash_Flow` | FY2026 actual rollup + FY2027 forecast, liquidity alert tiers, burn rate & runway |
| `AR_Aging` | 0–30/31–60/61–90/90+ aging, DSO, collection rate |
| `AP_Analysis` | Payables aging, DPO, working capital, cash conversion cycle |
| `Scenario_Analysis` | Best/Base/Worst side-by-side comparison |
| `KPI_Summary` | Executive KPI matrix — formula, value, target, interpretation |
| `Dashboard` | KPI cards, live charts, heatmap review protocol |

All figures are formula-driven from `Raw_Data` (`SUMIFS`, `INDEX/MATCH`-style lookups) — change a transaction and every downstream tab recalculates.

## 4. Cash Flow Schedule (Section 6)

FY2026 opens at $850,000 and closes the year around **$540K**, staying in the "Healthy" liquidity tier every month. The FY2027 Base Case forecast tells a different story: liquidity status slides from **Healthy → Watch → Critical** by mid-year, and modeled closing cash approaches roughly breakeven by December — driven by hosting/COGS costs and fixed costs growing faster than the modeled revenue growth rate.

## 5. Budget vs. Actual Variance (Sections 7–8)

FY2026 department spend came in **1.3% under total annual budget** — a healthy aggregate — but it masks two departments running over: **IT** (+0.3%) and **CapEx** (+1.5%), both flagged Unfavorable, while Marketing, HR, Operations, Admin, and Finance all landed Favorable (under budget).

## 6. Scenario Results (Section 14)

| Metric (FY2027) | Worst Case | Base Case | Best Case |
|---|---|---|---|
| Total Revenue | ~$2.06M | ~$2.40M | ~$2.58M |
| Total Outflows | ~$3.10M | ~$2.94M | ~$2.87M |
| Net Cash Flow | ~-$1.04M | ~-$0.55M | ~-$0.29M |
| Closing Cash | ~-$0.50M | ~-$0.01M | ~+$0.25M |

The uncomfortable finding: **even the Best Case doesn't fully close the gap.** Revenue acceleration alone doesn't fix this — cost structure discipline (COGS scaling with revenue, fixed cost growth) is the binding constraint, not top-line growth.

## 7. Working Capital & AR/AP

- **DSO:** ~59 days (target: <45) — a real collection bottleneck against Net 30/45 terms.
- **DPO:** ~23 days — payables are being settled faster than necessary; there's room to extend terms and preserve cash.
- **Cash Conversion Cycle:** ~36 days.
- **Net Working Capital:** ~$195K positive.

## 8. Key Insights

1. Even in the Best Case revenue scenario, cash outflows still exceed inflows — the model shows this is a cost problem, not a growth problem.
2. Liquidity is projected to cross into "Critical" territory by mid-FY2027 under the Base Case, well before cash is fully depleted — the alert exists specifically to give leadership lead time.
3. DSO (~59 days) is meaningfully above the 45-day target, while DPO (~23 days) is conservative — working capital is being financed by the company, not by its suppliers.
4. IT and CapEx are the only two departments running over their FY2026 budget, making them the first place to look for near-term savings.
5. Hosting/software costs that scale directly with revenue mean that revenue growth alone doesn't proportionally improve margin — gross margin needs a structural review, not just top-line acceleration.
6. Aggregate budget performance (-1.3% variance, i.e. under budget) looks healthy at the company level but hides department-level overspending — a reminder that FP&A review has to happen below the topline.
7. The Worst Case scenario depletes cash well before year-end, with a negative implied runway — underscoring the value of a live burn-rate and runway tracker, not just a static annual budget.
8. Positive net working capital (~$195K) is a cushion, but it's driven more by low DPO than by strong AR collection — renegotiating supplier terms is a lower-risk lever than chasing collections.
9. The FY2026 actuals stay "Healthy" all year while the FY2027 forecast does not — a reminder that trailing performance is not a reliable predictor of forward liquidity once growth assumptions and cost scaling are modeled explicitly.
10. Because ~68% of revenue is billed annually upfront, the cash conversion cycle is naturally favorable — but that advantage is being offset by cost growth, not enhanced by it.

## 9. Strategic Recommendations

| # | Recommendation | Estimated Cash Impact |
|---|---|---|
| 1 | Tighten AR collections toward the 30/45-day terms actually on the contract | Could recover ~$50–80K in freed-up working capital |
| 2 | Renegotiate select vendor terms from Net 30 to Net 45 | ~$20–30K in deferred outflow timing, no margin cost |
| 3 | Freeze discretionary IT and CapEx spend for one quarter pending review | ~$40–60K in near-term outflow reduction |
| 4 | Re-baseline hosting/COGS contracts against usage growth rather than flat scaling | Improves gross margin trajectory over 2–3 quarters |
| 5 | Defer non-critical CapEx (equipment refreshes) into a later, cash-healthier quarter | ~$25–40K in deferred outflow |
| 6 | Activate or pre-negotiate a revolving credit facility before the Critical-tier months hit | Protects against a hard cash shortfall; low cost if unused |
| 7 | Introduce a rolling 13-week cash forecast in addition to the annual model, refreshed monthly | Earlier detection, smaller corrective moves needed |
| 8 | Tie department budget overages (>5%) to a mandatory variance memo and corrective plan | Improves cost discipline without a blanket spending freeze |

## 10. Dashboard Layout

- **Top:** KPI cards — Revenue, Inflows, Outflows, Net Cash, Closing Cash, Budget Variance %.
- **Middle:** Inflow vs. outflow trend, budget vs. actual by department, closing cash trend, department expense mix.
- **Bottom:** AR aging buckets, AP schedule, cash runway gauge, scenario comparison, Critical/Watch/Healthy alert banners.
- **Filters:** Month, Quarter, Department, Cost Category, Scenario, Transaction Type.

## 11. Tech Stack

- **Core model:** Excel (this workbook) — portable to Google Sheets with minor formula adjustments.
- **Visualization:** Power BI or Tableau for a refreshable, filterable version of the Dashboard tab.
- **Advanced analytics:** SQL for querying the transaction table at scale; Python (pandas) for scenario Monte Carlo runs and automated variance commentary.

## 12. Repository Structure

```
/data/                 - Raw_Data export (CSV), data dictionary
/financial-model/      - The Excel workbook (source of truth)
/forecast/             - Revenue_Forecast & Expense_Forecast exports, assumptions log
/budget-analysis/      - Budget vs. Actual exports, variance heatmap export
/dashboard/            - Power BI/Tableau file (if built), dashboard spec
/screenshots/          - Dashboard, KPI summary, scenario comparison screenshots
/docs/                 - This README, data quality log, methodology notes
README.md
```

## 13. Skills Demonstrated

`FP&A` · `Cash Flow Forecasting` · `Budget vs. Actual Variance Analysis` · `Working Capital & Cash Conversion Cycle` · `Financial Modelling` · `Scenario Analysis` · `Excel (SUMIFS, INDEX/MATCH, conditional formatting)` · `Executive Dashboard Design`
