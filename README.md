# epitope-threshold-analysis-supplement
Supplemental threshold evaluation for paper: Prediction of B-cell Conformational Epitope With Multiple-Modal Fusion Strategy


This repository provides additional threshold calibration and evaluation results for the paper:
**"Prediction of B-cell Conformational Epitope With Multiple-Modal Fusion Strategy"**, accepted at [ICBBT,2025]  
Authors: [Tao Chuan Shih]
Original DOI: [TBD]


- Thresholds include:
  - Youden’s J (from ROC curve): The original thrheshold for original paper
  - F1-optimal: Supplemental threshold





Table III.
| Method            | Threshold(Type)| Precision | Recall | Specificity | F1-score | AUROC | PR-AUC | MCC    |
|-------------------|----------------|-----------|--------|-------------|----------|--------|--------|--------|
| EGNN + SaProt-Cross-DT | Youden’s J      | 0.7340    | 0.1649 | 0.2649      | 0.7338   | 0.8067 | 0.2331 | 0.2556 |
| EGNN + SaProt-Cross-DT | F1-optimal      | 0.4485    | 0.2185 | 0.2938      | 0.8851   | 0.8067 | 0.2331 | 0.2421 |
| BepiPred 3.0      | 0.1512         | 0.6031    | 0.1649 | 0.2590      | 0.7812   | 0.7670 | 0.2002 | 0.2233 |
| DiscoTope 3.0     | 0.89           | 0.4638    | 0.1879 | 0.2675      | 0.8564   | 0.7854 | 0.2088 | 0.2155 |
| GraphBepi         | 0.1763         | 0.3607    | 0.1884 | 0.2475      | 0.8886   | 0.7438 | 0.1803 | 0.1864 |
| EpiGraph          | 0.1481         | 0.2382    | 0.2114 | 0.2240      | 0.9363   | 0.7423 | 0.1741 | 0.1651 |


## Notes
- 
- Model code and weights are not publicly released at this time.
- Evaluation results are computed from fixed validation/test splits as used in the original paper.
