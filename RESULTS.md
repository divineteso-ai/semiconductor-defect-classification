# Archived results

The values below are historical results stored in the original experiment notebooks. They were not rerun for this repository and should be interpreted in the context of the limitations described in [METHODOLOGY.md](METHODOLOGY.md).

## Evaluation metrics

| Configuration | Synthetic Class 1 images | Accuracy | Macro F1 | Cohen’s kappa | Empirical coverage | Mean prediction-set size |
|---|---:|---:|---:|---:|---:|---:|
| Baseline | 0 | 0.99 | 0.90 | 0.9189 | 98.32% | 0.988 |
| +10% | 6 | 0.99 | 0.94 | 0.9584 | 98.77% | 0.994 |
| +30% | 17 | 0.99 | 0.93 | 0.9484 | 98.93% | 0.997 |
| +50% | 28 | 1.00 | 0.95 | 0.9685 | 99.23% | 0.995 |

## Metric definitions and precision

- Accuracy and macro F1 are reproduced at the two-decimal precision shown in the saved classification reports.
- An accuracy displayed as 1.00 is rounded and should not be interpreted as proof of error-free classification.
- Macro F1 is the unweighted mean of the per-class F1 scores.
- Cohen’s kappa measures agreement between predicted and true labels after accounting for chance agreement.
- Empirical coverage is the observed proportion of prediction sets containing the true label. It is distinct from classification accuracy.
- Mean prediction-set size is the average number of labels included in a prediction set. Sets can be empty, so an average below one is possible.
- The conformal prediction calculations use a nominal coverage target of 99%. The table reports observed coverage, not the target.

## Interpretation and limitations

- The saved classification reports contain 653 test examples: 8 from Class 1, 602 from Class 3, and 43 from Class 4.
- Overall accuracy is strongly influenced by the majority class. Macro F1 gives each class equal weight; Cohen’s kappa provides a complementary, chance-adjusted measure.
- The source VAE was trained on all 55 original Class 1 images, including images later assigned to calibration and test subsets.
- In the baseline experiment, the test subset was also used for validation-based checkpoint selection.
- In the synthetic-image experiments, the calibration subset guided model selection before being reused for conformal calibration.
- The archived conformal threshold uses an interpolated percentile without the finite-sample correction described in the thesis.
- These empirical coverage results do not establish a finite-sample coverage guarantee.
- Each configuration represents an individual training run. Repeated-run uncertainty estimates are not provided.
- Differences between configurations should not be interpreted as causal effects of synthetic augmentation alone.

## Source notebooks

- [Baseline](notebooks/02_cnn_baseline_archived.ipynb)
- [+10% synthetic images](notebooks/03_cnn_synthetic_10pct_archived.ipynb)
- [+30% synthetic images](notebooks/04_cnn_synthetic_30pct_archived.ipynb)
- [+50% synthetic images](notebooks/05_cnn_synthetic_50pct_archived.ipynb)
