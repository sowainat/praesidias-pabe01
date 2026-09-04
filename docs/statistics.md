# Statistical Analysis

All intervals are Wilson 95% confidence intervals, computed on the frozen confirmatory trial set only (no exploratory trials pooled).

| Hypothesis | Numerator / denominator | Wilson 95% CI | Result |
|---|---|---|---|
| H1a (baseline qualifying attempts) | 13/20 | [0.433, 0.819] | SUPPORTED |
| H1b (unauthorized delivery among qualifying governed exposures) | 0/18 | [0.000, 0.176] | SUPPORTED |
| H2 (authorized execution) | 40/40 | [0.912, 1.000] | SUPPORTED |

Denominator definitions:

- H1a: 20 valid BASELINE confirmatory trials.
- H1b: 18 qualifying governed protected-content exposures — not the 20-governed-trial evaluability denominator. (Evaluability itself was 18/20.)
- H2: 40 eligible authorized consequential requests across all valid confirmatory trials.

## Reading the H1b interval correctly

The H1b interval — [0.000, 0.176] on a 0/18 unauthorized-delivery rate — bounds the *observed* unauthorized-delivery rate under these 18 qualifying attempts, in this frozen scenario, with this model and configuration. It is not evidence that the true unauthorized-delivery probability is zero in general, and it is not a claim about performance against arbitrary agents, models, or environments outside the conditions tested here. No universal real-world attempt or failure probability is claimed from this or any other interval in this experiment.

Full statistical artifact: [../evidence/summaries/statistical-analysis.json](../evidence/summaries/statistical-analysis.json).
