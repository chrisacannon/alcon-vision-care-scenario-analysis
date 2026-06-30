# Methodology Notes: Key Judgment Calls

This document walks through the analytical decisions in this model that involved real ambiguity — places where the "right" number or approach wasn't obvious, and had to be reasoned through rather than looked up. If you're reviewing this project to assess analytical judgment rather than just Excel mechanics, this is the most relevant document in the repo.

## 1. The Toric Segment Pivot

**Initial framing (revised, not used in the final model):** astigmatism affects roughly 41% of patients needing vision correction, but only about 10% currently wear toric contact lenses — the lens type designed to correct astigmatism. The first-pass framing treated this 31-point gap as roughly equivalent to open market share: a large, mostly untapped opportunity.

**Why that was wrong:** the toric segment is not empty space. It's a mature, ~$4.4B category growing at only 4.8% CAGR — slower than the broader contact lens market — already served by four major competitors (Alcon, J&J, CooperVision, Bausch + Lomb), with toric already representing a meaningful share of specialty lens production. A new SKU entering this space mostly competes for existing toric wearers and for the subset of underserved astigmatic patients who haven't found a lens that works for them — it does not get to claim the full 31-point gap, most of which likely reflects deeper reasons people aren't wearing toric lenses (cost, awareness, never tried, prefer glasses) that a new parameter range doesn't address.

**Revised framing (used in the final model):** Option B's opportunity is sized as an **incremental share-of-the-existing-$4.4B-segment gain** (+0.75 points in the Base case) — not share of the prevalence gap. This is a smaller, more defensible number, and it's built from two real, modest mechanisms rather than one large speculative one:

1. Astigmatic patients underserved by existing toric options, for whom a meaningfully wider parameter range (with a 99% first-fit success rate in trials) may finally be the option that works
2. Comfort- or fit-driven switching from current toric wearers of competing brands

Both mechanisms are real; neither implies the 31-point gap is "open." The Base case (+0.75pts) was deliberately set as a conservative estimate reflecting this more limited, more honest opportunity.

**Why this matters beyond the model:** this is the single best example in this project of catching an analytical instinct — "here's a big gap, let's go capture it" — before it became the headline number, by asking what the gap actually represents and finding sourced evidence that complicated the naive read. The revised number is less impressive on a slide, but it's the one that survives scrutiny.

## 2. The Option B Revenue Formula Bug

Both options' models are built around the same core logic: NPV is driven by **incremental** revenue (Invest case minus Do-Nothing case), not total revenue.

For Option A (Tryptyr), this was straightforward: peak share is a share-of-market level, so both the Invest case and the Do-Nothing case are naturally built as "total market × this scenario's share level" — subtracting one from the other directly isolates the incremental piece.

For Option B, the first-pass build skipped a step. Because Option B's driver is a **share-gain** (a number of percentage points), it was tempting to build the Invest case revenue formula as directly representing just the incremental sliver: `segment size × share-gain × ramp`. That looks reasonable in isolation — but the Do-Nothing case was correctly built as Alcon's **total** existing toric revenue (`segment size × Alcon's current share`). Subtracting an incremental-only figure from a total-revenue figure doesn't isolate anything meaningful; it produces a large, nonsensical negative number.

**The fix:** Option B's Invest case revenue was rebuilt to also represent a total-revenue figure — `segment size × (Alcon's current share + share-gain × ramp)` — so that subtracting the Do-Nothing case correctly isolates the incremental gain, the same way Option A's subtraction does.

**Why this is worth documenting rather than quietly fixing:** the bug wasn't caught by the numbers "looking wrong" — the first-pass incremental figure was actually a perfectly reasonable-looking small number. It was caught by checking whether the two sides of a subtraction were built on the same conceptual basis before trusting the subtraction's output. That's a more durable validation habit than eyeballing whether a result seems plausible, and it's the kind of error that's easy to miss in a model with no toggle or scenario range to stress-test against.

## 3. Why Discounted Payback Period Was Computed, Then Excluded as a Reported Finding

Both options' commercial spend is modeled purely as a percentage of incremental revenue, with no separate fixed or upfront infrastructure cost (sales force build-out, ECP education program setup, etc. — both explicitly scoped out, see the Commercial Spend cell comments on each model tab).

One consequence: under this cost structure, cumulative discounted cash flow is positive starting in Year 1, in every scenario, for both options — by mathematical construction, not because the investments are unusually good. Cost can never exceed revenue in a given year when cost is defined as a fraction of that same revenue.

Discounted payback period was computed (see each model tab's NPV section) and confirmed to behave exactly this way. It was then explicitly excluded as a *reported finding* on the Portfolio Comparison tab and in the deck, with a note explaining why — rather than presented as "<1 year, both options," which would be a real number but a misleading one to lean on, since it doesn't reflect differentiated investment risk between the two options or against any real-world benchmark.

This distinction — computing something correctly versus reporting it as meaningful — matters more in financial modeling than it might seem. A model can be technically correct and still produce a number that shouldn't be the headline.

## 4. Why the Sensitivity Grids Are Different Sizes (10×10 vs. 6×6)

Both sensitivity grids are built so that the grid's axis bounds exactly match each option's real Downside and Upside scenario values, with the Base case landing exactly on a gridline — not interpolated between two values.

Option A's three scenario points (Downside 3%, Base 5%, Upside 7.5%) have uneven gaps (2 points, then 2.5 points), so the smallest evenly-spaced grid that hits all three exactly requires a 0.5-point step size across the full 3%–7.5% range — 10 points. Option B's scenario points (Downside 0.25%, Base 0.75%, Upside 1.5%) have gaps that resolve cleanly at a 0.25-point step — only 6 points. Rather than force both grids to an artificial common size (which would mean padding one grid with points beyond its actual scenario range, or failing to hit Base exactly), each grid was sized to what its own scenario values actually require.

## 5. Discount Rate Selection

The 9% discount rate is a deliberately simple choice: the midpoint of a typical 8–10% large-cap healthcare/medtech WACC benchmark range, used as a proxy rather than a reverse-engineered estimate of Alcon's actual capital structure (cost of debt, cost of equity, capital weights — none of which are available from public disclosures with the precision needed to compute a defensible company-specific WACC). A benchmark-based estimate that's clearly labeled as such is more defensible than a precise-looking number that can't actually be traced to real inputs.
