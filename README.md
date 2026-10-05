# network intrusion detection using machine learning

a machine learning pipeline for identifying malicious network traffic using a cicids2017-based dataset. this project evaluates classical machine learning approaches including a scratch implementation of k-nearest neighbours, decision trees, principal component analysis, cross-validation, error analysis and model robustness testing.

## overview

network intrusion detection involves identifying malicious activity from network traffic patterns.

this project explores whether classical machine learning models can accurately distinguish between benign and malicious network flows while maintaining strong generalisation performance.

the complete dataset contains **851,388 network flows with 52 numerical input features** and a balanced binary target.

## key results

the selected model was a decision tree with a maximum depth of 10.

| metric | result |
|---|---:|
| accuracy | 99.36% |
| precision | 99.75% |
| recall | 98.97% |
| f1-score | 99.36% |
| roc-auc | 99.84% |
| mean cross-validation f1 | 99.35% |

on the 18,000-example test set, the selected model produced:

- 8,978 true negatives
- 8,907 true positives
- 22 false positives
- 93 false negatives

the bootstrap 95% confidence interval for the f1-score was approximately **99.22% to 99.47%**.

## methodology

the project follows the following experimental pipeline:

1. dataset inspection and validation
2. stratified sampling
3. train/test splitting
4. feature standardisation
5. naive majority-class baseline
6. k-nearest neighbours implemented from scratch
7. decision tree model comparison
8. cross-validation
9. sample-size sensitivity analysis
10. principal component analysis
11. error analysis
12. roc and precision-recall analysis
13. bootstrap confidence interval estimation

## models evaluated

### naive baseline

a majority-class baseline was used as a reference point.

accuracy: **50%**

### k-nearest neighbours

knn was implemented from scratch rather than using sklearn's classifier.

| model | accuracy | f1-score |
|---|---:|---:|
| knn k=3 | 97.80% | 97.75% |
| knn k=5 | 97.70% | 97.65% |
| knn k=7 | 97.40% | 97.35% |

### decision trees

| model | accuracy | f1-score |
|---|---:|---:|
| depth 3 | 94.68% | 94.68% |
| depth 5 | 98.39% | 98.38% |
| depth 10 | **99.36%** | **99.36%** |
| unrestricted | 99.71% | 99.71% |

although the unrestricted tree achieved the highest raw test performance, the depth-10 model was selected for deeper analysis to maintain a better balance between predictive performance and model complexity.

## principal component analysis

pca reduced the feature space from:

**52 features → 18 principal components**

while retaining approximately:

**95.18% of explained variance**

the reduced feature representation produced competitive performance, although predictive accuracy decreased slightly compared with the original feature space.

## sample-size analysis

model performance remained strong across different training sample sizes.

| sample size | accuracy | f1-score |
|---|---:|---:|
| 5,000 | 99.00% | 99.00% |
| 10,000 | 99.10% | 99.09% |
| 30,000 | 99.23% | 99.23% |
| 60,000 | 99.36% | 99.36% |

## technologies

- python
- numpy
- pandas
- matplotlib
- scikit-learn
- jupyter notebook

## project structure

```text
network-intrusion-detection/
├── assets/
├── data/
│   └── README.md
├── docs/
│   └── network_intrusion_detection_report.pdf
├── notebooks/
│   └── network_intrusion_detection.ipynb
├── .gitignore
├── README.md
└── requirements.txt