# Private Credit / Direct Lending Deal Underwriting Model

A Python-based credit underwriting engine that replicates the core workflow used by middle-market direct lenders and private credit funds to evaluate a prospective term loan.

## What It Does

- Pulls 5 years of borrower financials live from the **SEC EDGAR XBRL API** (with an automatic synthetic-data fallback if EDGAR is unreachable)
- Computes historical leverage, coverage, and margin trends
- Structures a term loan: sizing off LTM EBITDA, pricing, amortization, and a discretionary cash-flow sweep
- Projects 5-year cash flow and **Debt Service Coverage Ratio (DSCR)**
- Stress-tests the deal across **Base / Downside / Severe Downside** scenarios
- Runs a **5,000-path Monte Carlo simulation** to quantify covenant-breach probability
- Auto-generates a one-page **credit memo** with a preliminary recommendation

## Sample Output

| DSCR by Scenario | Monte Carlo Distribution |
|---|---|
| Line chart of DSCR across 5 years for Base/Downside/Severe Downside vs. covenant floor | Histogram of 5,000 simulated minimum-DSCR outcomes |

*(Run the notebook once and these render inline — see `/charts` if you export static PNGs.)*

## How to Run

1. Open `Private_Credit_Underwriting_Model.ipynb` in Google Colab
2. Run all cells (`Runtime → Run all`)
3. Edit `CONFIG` in Section 1 to point at a different borrower ticker or change loan terms
4. Re-run — the entire pipeline (data → structuring → projection → Monte Carlo → memo) regenerates end to end

No API keys required. SEC EDGAR is free and keyless (just needs a descriptive User-Agent header, already set in `CONFIG`).

## Tech Stack

`pandas` · `numpy` · `matplotlib` · `requests`

## Project Structure

```
├── Private_Credit_Underwriting_Model.ipynb   # main notebook
├── requirements.txt
└── README.md
```

## Disclaimer

Built for educational/portfolio purposes. Uses a public company as a borrower "proxy" to demonstrate the modeling framework — not a real underwriting analysis of any actual credit, and not investment advice.
