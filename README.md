# epitope-threshold-analysis-supplement
Supplemental for paper: Prediction of B-cell Conformational Epitope With Multiple-Modal Fusion Strategy

This repository provides additional threshold calibration and evaluation results for the paper:
**"Prediction of B-cell Conformational Epitope With Multiple-Modal Fusion Strategy"**, accepted at [ICBBT,2025]  
Authors: [Tao Chuan Shih]
Original DOI: [TBD]

##### Notes
- Model code and weights are not publicly released at this time.

**Re-evalutaion of the thresholds**

Table III.
- Thresholds include:
  - Youden’s J (from ROC curve): The original thrheshold for original paper
  - F1-optimal: Supplemental threshold

| Method            | Threshold(Type)| Recall    | Precision | Specificity | F1-score | AUROC | PR-AUC | MCC    |
|-------------------|----------------|-----------|--------|-------------|----------|--------|--------|--------|
| EGNN + SaProt-Cross-DT | Youden’s J(0.5475)      | 0.7340    | 0.1649 | 0.2649      | 0.7338   | 0.8067 | 0.2331 | 0.2556 |
| EGNN + SaProt-Cross-DT | F1-optimal(0.7688)      | 0.4485    | 0.2185 | 0.2938      | 0.8851   | 0.8067 | 0.2331 | 0.2421 |
| BepiPred 3.0      | 0.1512         | 0.6031    | 0.1649 | 0.2590      | 0.7812   | 0.7670 | 0.2002 | 0.2233 |
| DiscoTope 3.0     | 0.89           | 0.4638    | 0.1879 | 0.2675      | 0.8564   | 0.7854 | 0.2088 | 0.2155 |
| GraphBepi         | 0.1763         | 0.3607    | 0.1884 | 0.2475      | 0.8886   | 0.7438 | 0.1803 | 0.1864 |
| EpiGraph          | 0.1481         | 0.2382    | 0.2114 | 0.2240      | 0.9363   | 0.7423 | 0.1741 | 0.1651 |


##### Notes
- Evaluation results are computed from fixed validation/test splits as used in the original paper.
- The main description of the paper depicts a higher AUROC and PR-AUC indicates that the model has a higher ability to rank the positive samples, but the original paper used Youden's J index (TPR - FPR maximum) to select the threshold for a fair comparison and did not take the problem of extreme imbalance of the samples into consideration, which resulted in a tendency to over-predict the positive samples under this threshold, thus lowering specificity and increasing recall.We used the threshold of the F1-score maximum in the supplementary data for the re-analysis.In the supplementary data, the threshold corresponding to the maximum value of F1-score is used for analysis, which can better balance precision and recall, and increase specificity, better reflecting the actual ranking ability of the model and echoing with the overall performance of AUROC and PR-AUC.

**Pathogen independent dataset**

Table S1.
Pathgen idenpent dataset

| Method                         | Recall | Precision | F1-score | SP     | AUROC  | PR-AUC | MCC    |
|--------------------------------|--------|-----------|----------|--------|--------|--------|--------|
| EGNN SaProt-Cross-ST (F1-optimal / 0.8098) | 0.3090 | 0.1910    | 0.2361   | 0.9122 | 0.7229 | 0.1714 | 0.1776 |
| EGNN SaProt-Cross-DT (F1-optimal / 0.7688) | 0.3790 | 0.1979    | 0.2600   | 0.8969 | 0.7254 | 0.1791 | 0.2058 |
| Bepipred 3.0 (0.1512)          | 0.6560 | 0.1021    | 0.1767   | 0.6131 | 0.6972 | 0.1460 | 0.1331 |
| DiscoTope 3.0 (0.89)           | 0.4198 | 0.1296    | 0.1981   | 0.8108 | 0.6952 | 0.1156 | 0.1390 |
| GraphBepi (0.1763)             | 0.3965 | 0.1635    | 0.2315   | 0.8638 | 0.7430 | 0.1707 | 0.1758 |
| EpiGraph (0.1481)              | 0.2382 | 0.2028    | 0.2254   | 0.9331 | 0.7257 | 0.1474 | 0.1684 |

##### Notes
- Evaluation results are computed from fixed validation/test splits as used in the original paper.
- Pathogen independent dataset was derieved from another curretly WIP, the logic behind the datasets is: SAbDab (May 2025 snapshot) as the primary source of a large number of experimentally resolved antibody-antigen complex structures; AbDb (July 2024 snapshot) as a supplement to make up for the structures that were not captured by SAbDab. To ensure the quality of the data, the following filtering and classification criteria were used: Resolution requirement: only X-ray structures with a resolution of ≤ 3.0 Å or Cryo-EM structures with a clear resolution annotation were included; Structural completeness: The structure should contain both the heavy chain and light chain of the antibody and the third(antigen) chain; the length of the antigen chain should be between 50 and 1000 amino acids; Antigenic biology filtering: Artificial proteins, functional proteins unrelated to immune response, and protein structures with a mechanism or structural similar to MHC are exclude; Training set identity check: MMseqs2 was used for sequence comparison on the training sets of CE prediction models, and labelled the number of times the PDB entries and similar PDBs appeared in the datasets of each CE predictor. Based on the sequential repetition and functions, we further classified the data into two primary datasets and one supplementary dataset: Full set (53 complexes): This dataset serves as the primary benchmark for conformational epitope prediction. The data is mainly based on no repetition antigens with the training data of the existing models (excluded if sequence identity >0.7), but also allows partial sequence similarity with the training set, retains only those pairs that show one-to-one 100% similarity with the training data. For each predictor evaluated, any test sequence that was 100% identical to a sequence in its training set was excluded at runtime; Pathogen subset (21 complexes): To further analyze the ability of the model to generalize on pathogen antigens, complexes derived from viruses, bacteria, and toxins were selected from the Full Set, excluding self-antigen。Three PDBs(6z2l, 8jkf and 8yxi) were removed due to the overly 70% sequence identity between it's sequence and the dataset for this study throguht blastp program.
