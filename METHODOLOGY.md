# Methodology and limitations

## Overview

This project compares a CNN baseline with three VAE-augmented training configurations for SEM defect classification. The task uses Classes 1, 3, and 4 of the Carinthia dataset. Class 1 is treated as the minority class.

The VAE generates synthetic Class 1 images. The CNN experiments add selected synthetic images to the training subset and compare the resulting performance with a baseline trained only on original images.

## Data split

The original images are divided into training, calibration, and test subsets using a 70/15/15 stratified split.

- Training subset: used to fit the CNN.
- Calibration subset: used for model selection and later for conformal calibration.
- Test subset: used for final evaluation.

The synthetic images are added only to the training subset. The augmentation percentages are based on the 55 original Class 1 images:

| Configuration | Synthetic images | Relative amount |
|---|---:|---:|
| Baseline | 0 | 0% |
| +10% | 6 | 10% |
| +30% | 17 | 30% |
| +50% | 28 | 50% |

## Model architecture

The CNN uses a frozen ImageNet-pretrained ResNet50V2 backbone. Only the classification head is trained. The head uses global average pooling, dropout, and a three-class softmax output.

Training-time augmentation includes geometric and photometric transformations. The backbone is not fine-tuned.

## Conformal prediction

The notebooks compute a nonconformity score for each calibration example:

\[
s_i = 1 - \hat{p}_{y_i}(x_i)
\]

Here, \(\hat{p}_{y_i}(x_i)\) is the model’s predicted probability for the true class \(y_i\).

The archived implementation selects a threshold using NumPy’s default interpolated 99th percentile. It does not apply the finite-sample correction described in the thesis. Therefore, the reported empirical coverage should not be interpreted as a verified finite-sample coverage guarantee.

Prediction sets are formed by including labels whose scores do not exceed the calibration threshold. A prediction set can be empty.

## Important limitations

The notebooks preserve the original experimental workflow. The following limitations should be considered when interpreting the results:

- The VAE was trained on all 55 original Class 1 images, including images later assigned to calibration and test subsets.
- The calibration subset was used for model selection before being reused for conformal calibration.
- In the baseline notebook, the test subset was also used for validation-based checkpoint selection.
- The final comparison uses manually copied historical metrics, not a fresh joint evaluation.
- No repeated training runs or uncertainty estimates are included.
- The archived results are historical outputs, not results from a newly validated execution environment.

## Intended use

This repository is intended to make the original workflow and archived results transparent. It is not intended as a claim that the reported performance generalizes beyond the specific data split, hardware, software environment, and experimental configuration used in the original study.
