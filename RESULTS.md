# Archived results

The values below are historical results stored in the original notebooks. They were not rerun for this repository and should be interpreted in the context of the documented methodological limitations.

| Configuration | Synthetic Class 1 images | Accuracy | Macro F1 | Cohen’s kappa | Empirical coverage | Mean prediction-set size |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 0 | _to be added_ | _to be added_ | _to be added_ | _to be added_ | _to be added_ |
| +10% | 6 | _to be added_ | _to be added_ | _to be added_ | _to be added_ | _to be added_ |
| +30% | 17 | _to be added_ | _to be added_ | _to be added_ | _to be added_ | _to be added_ |
| +50% | 28 | _to be added_ | _to be added_ | _to be added_ | _to be added_ | _to be added_ |

## Notes

- “Empirical coverage” is the observed proportion of prediction sets containing the true label.
- “Mean prediction-set size” is descriptive and must be interpreted together with coverage.
- These metrics do not establish a finite-sample coverage guarantee.
- The configurations differ in more than the number of synthetic images: each uses its own training run and checkpoint selection.
- Differences between rows should therefore not be interpreted as causal effects of augmentation alone.
