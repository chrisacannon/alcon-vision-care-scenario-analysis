# Alcon Vision Care Franchise — FY27 Portfolio Investment Analysis

**An independent portfolio case study by [Chris Cannon](https://github.com/your-github-handle)**

A self-initiated financial modeling and strategy exercise evaluating two real, current investment opportunities for Alcon's Vision Care Franchise, built to demonstrate the analytical toolkit described in Alcon's [Senior Manager, Global Business Strategy & Planning](https://alcon.wd5.myworkdayjobs.com/careers_alcon) job description: scenario modeling with toggle logic, sensitivity analysis, and structured portfolio prioritization (market attractiveness / right-to-win).

This was not a take-home assignment — it was built unprompted, from public information, as a way to demonstrate the work itself rather than just describe it.

---

## The Case

Alcon's Vision Care Franchise has incremental FY27 investment capacity. Two independent, real opportunities are evaluated on their own merits — this is a portfolio sequencing exercise, not a "pick one" decision:

- **Option A — Tryptyr Commercial Acceleration**: incremental sales force / DTC investment to accelerate share capture for Tryptyr, Alcon's first-in-class (TRPM8-receptor) dry-eye treatment, launched Q3 2025.
- **Option B — Contact Lens Parameter Expansion**: incremental ECP education/marketing investment to extend PRECISION1 / DAILIES TOTAL1 / TOTAL30 parameter ranges within the toric (astigmatism) contact lens segment.

All market sizing, growth rates, and product details are drawn from Alcon's public disclosures (Q1 2026 earnings, product launch announcements, prescribing information) and third-party industry sources — not from any non-public materials. Full sourcing is documented inline in the model (see [Sourcing & Methodology](#sourcing--methodology) below).

## What's in This Repo

| Path | Contents |
|---|---|
| `model/` | Full Excel workbook — assumptions, two scenario-driven NPV models, two sensitivity analyses, portfolio comparison |
| `deck/` | 12-slide companion deck — executive summary + full appendix detail |
| `docs/` | Write-up of key analytical decisions and judgment calls (this is the most interesting part if you only have a few minutes) |

**Start here if you want the headline:** open the deck (`deck/Alcon_VisionCare_Portfolio_FY27.pptx`), slides 1–5.

**Start here if you want to see the work:** open the model (`model/Alcon_Vision_Care_Franchise_FY27_Portfolio_Investment_Analysis.xlsx`) and read `docs/methodology.md` alongside it.

## Headline Results

| | Option A: Tryptyr | Option B: Lens Expansion |
|---|---|---|
| 5-yr NPV, Downside | $0.256B | $0.034B |
| 5-yr NPV, **Base** | **$0.589B** | **$0.102B** |
| 5-yr NPV, Upside | $1.006B | $0.203B |
| Commercial spend ratio | 22.5% of incremental revenue | 12.5% of incremental revenue |
| Market Attractiveness | Medium-High | Low-Medium |
| Right-to-Win | Medium | High |

**Recommendation:** fund both — they're independent and NPV-positive in every tested scenario. If capacity is constrained, prioritize Option A first: its patent-protected window erodes regardless of investment timing, while Option B's opportunity is durable and doesn't decay on a clock. Full reasoning in the deck (slide 5) and the model's `Portfolio_Comparison` tab.

## Model Structure

- **`Cover_Assumptions`** — all sourced inputs, Base/Upside/Downside scenario tables for both options, shared structural decisions (5-yr horizon, 9% discount rate proxy, do-nothing baseline methodology)
- **`Option_A_Tryptyr`** — revenue build (market-growth-adjusted), do-nothing baseline, commercial spend, full NPV chain with a live Base/Upside/Downside toggle, plus a 10×10 sensitivity grid (peak share × commercial spend ratio)
- **`Option_B_LensExpansion`** — same structure, adapted for a share-of-segment-gain mechanic rather than share-of-market; 6×6 sensitivity grid
- **`Portfolio_Comparison`** — market attractiveness / right-to-win scoring (8 criteria across 2 dimensions), financial side-by-side, sequencing recommendation

**Modeling conventions used throughout:** blue text = hardcoded input, black text = same-sheet formula, green text = cross-sheet link. Every hardcoded assumption carries a cell comment citing its source or flagging it explicitly as a reasoned judgment call rather than a hard data point.

## Sourcing & Methodology

Every assumption in the model is documented at the cell level (see the `Source/Basis` column on each tab, plus cell comments). At a glance:

- Market sizing: Alcon Q1 2026 earnings disclosures; global dry-eye disease and toric lens segment data from industry sources
- Tryptyr clinical/tolerability data: Alcon prescribing information and COMET trial disclosures
- Discount rate, ramp curves, and several option-specific assumptions (e.g., Option B's share-of-segment gain, Alcon's estimated current toric share) are explicitly flagged as **reasoned judgment calls**, not sourced figures — and documented as such rather than presented with false precision

See `docs/methodology.md` for a walkthrough of the more interesting judgment calls, including:
- A real mid-build pivot: the initial framing of Option B's opportunity (a 41%-to-10% astigmatism/toric-adoption "gap") was revised after finding the toric segment is mature and competitively saturated, not open white space — and what that implies for how the opportunity should actually be sized and described
- A structural bug caught and fixed mid-build in Option B's revenue formula (comparing an incremental-only figure against a total-revenue figure), and what the fix reveals about validating model logic rather than just trusting that the numbers "look right"
- Why discounted payback period — a metric this model is fully capable of computing — was deliberately excluded as a reported finding, and why that's different from not knowing the answer

## A Decade-Old Connection

Coincidentally, this isn't my first project involving Alcon. In 2016, as part of a graduate consulting capstone, I worked on a different Alcon-related case: identifying ways to reinvigorate Alcon's laser vision correction (LASIK) business as its core customer base shifted generationally. That project is not included in this repo, but the throughline is the same: turning ambiguous, partially-sourced business questions into a structured, defensible recommendation.

## Tools

Built in Microsoft Excel and PowerPoint. No macros, no add-ins — everything is native formulas, conditional formatting, and data validation, built to be fully auditable by opening the file and clicking on cells.

---

*This project uses only publicly available information about Alcon and its products. It is an independent analytical exercise and is not affiliated with, endorsed by, or representative of any non-public Alcon data, strategy, or decision-making.*
