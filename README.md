# Patient Calibrated Dynamic Graph Fusion for Cross Patient EEG Seizure Detection

Author: ESMAIL IBRAHIM MOHAMMED AL NAKEEB
Student ID: 2598555
Program: Master of Science in Artificial Intelligence
University: Bahçeşehir University

## Project Description

This project implements a deep learning pipeline for cross patient EEG seizure detection using the CHB-MIT scalp EEG dataset. The main idea is to represent each EEG window as a dynamic brain connectivity graph, where EEG channels are graph nodes and correlation based relationships between channels are graph edges.

The project focuses on patient level generalization. Training, validation, and testing are performed on different patients to avoid data leakage from random EEG window splitting. In addition to standard dynamic graph learning, the project introduces patient specific graph calibration. Normal baseline graphs are estimated from reserved non seizure calibration windows and used to create patient calibrated graph representations.

The final method is a Validation Tuned Graph Ensemble that combines dynamic graph models and patient calibrated graph models using validation selected weights.

## Main Contribution

The main contribution of this project is a patient calibrated dynamic graph fusion approach for cross patient EEG seizure detection. Instead of only learning global EEG patterns, the model also uses patient specific normal baseline graph information. This allows the system to compare current EEG connectivity with the patient's normal graph behavior.

The final model achieved the best F1 score on the primary patient level test split and reduced false positives compared with the strongest individual graph baseline.

## Dataset

Dataset name: CHB-MIT Scalp EEG Database
Dataset source: PhysioNet
Dataset link: https://physionet.org/content/chbmit/1.0.0/

The raw EDF dataset files are not included in this submission because they are large. The notebook downloads the selected subset directly from PhysioNet.

Selected patients used in the final experiment:

* chb01
* chb02
* chb03
* chb05
* chb06
* chb07
* chb08
* chb10

For each selected patient, two seizure containing EDF recordings were downloaded when available.

## Project Files

The submitted package contains the following main components:

```text
1_Code/
    Patient_Calibrated_Dynamic_Graph_Fusion_EEG_Seizure_Detection.ipynb
    README.md

2_Results/
    Tables/
    Figures/
    Summaries/

3_Report/
    LaTeX project files
    Final report PDF

4_Poster/
    Final poster file
```

## Main Notebook

The main notebook is:

```text
Patient_Calibrated_Dynamic_Graph_Fusion_EEG_Seizure_Detection.ipynb
```

The notebook includes:

* Package installation
* Dataset download
* EEG preprocessing
* Window labeling
* Node feature extraction
* Dynamic graph construction
* Patient baseline graph calibration
* Traditional machine learning baselines
* MLP baseline
* Static GCN
* Dynamic GCN
* Dynamic GAT
* Patient Calibrated GAT
* Hybrid DPC GAT
* Validation Tuned Graph Ensemble
* Final evaluation
* Bootstrap testing
* Repeated patient split robustness testing
* Figures and result tables generation

## Required Environment

The project was designed to run in Google Colab.

Recommended environment:

```text
Python 3.10 or newer
Google Colab runtime
CPU runtime is acceptable
GPU runtime is recommended for faster training
```

Main Python libraries:

```text
numpy
pandas
scipy
scikit-learn
matplotlib
mne
torch
tqdm
requests
json
pathlib
```

Recommended package versions:

```text
numpy >= 1.24
pandas >= 2.0
scipy >= 1.10
scikit-learn >= 1.3
matplotlib >= 3.7
mne >= 1.6
torch >= 2.0
tqdm >= 4.65
requests >= 2.31
```

The notebook includes installation cells for the required packages. If running in Google Colab, run the notebook from top to bottom.

## How to Run the Project

1. Open the notebook in Google Colab.

2. Select the runtime:

```text
Runtime > Change runtime type > GPU
```

GPU is recommended but not strictly required.

3. Run all cells:

```text
Runtime > Run all
```

4. The notebook will automatically:

* Install required libraries
* Download the selected CHB-MIT EDF files
* Process EEG recordings
* Build graph representations
* Train all baseline and graph models
* Evaluate the final ensemble
* Save results, figures, and summary files

5. The generated outputs will be saved in the project results folder.

## Important Notes

The raw CHB-MIT EDF files are not submitted in the ZIP file because they are large. The notebook downloads the selected subset directly from PhysioNet.

The project uses a patient level split instead of a random window split. This is important because random splitting can create data leakage when EEG windows from the same patient appear in both training and testing.

Calibration windows from validation and test patients are used only for patient baseline graph estimation. They are not used when calculating validation or test performance.

## Final Model

The final selected model is:

```text
Validation Tuned Graph Ensemble
```

It combines predictions from selected graph based models, including Dynamic GCN, Dynamic GAT, Patient Calibrated GAT, and Hybrid DPC GAT variants.

## Main Results

Final ensemble performance on the primary patient level test split:

```text
Accuracy: 0.8628
Precision: 0.6840
Recall sensitivity: 0.9813
Specificity: 0.8142
F1 score: 0.8061
ROC AUC: 0.9836
False positive rate: 0.1858
False negative rate: 0.0187
```

Confusion matrix:

```text
True negatives: 425
False positives: 97
False negatives: 4
True positives: 210
```

The final ensemble achieved the best F1 score on the primary split and reduced false positives compared with Dynamic GCN, the strongest individual graph baseline.

## Baselines Compared

The following methods were compared:

* Logistic Regression EEG Features
* Random Forest EEG Features
* SVM RBF EEG Features
* MLP EEG Features
* Static GCN
* Dynamic GCN
* Dynamic GAT
* Patient Calibrated GAT
* Hybrid DPC GAT
* Validation Tuned Graph Ensemble

## Robustness Testing

The project includes two additional robustness checks:

1. Bootstrap analysis comparing the final ensemble with Dynamic GCN on the primary test split.
2. Repeated patient split testing using additional patient split seeds.

The bootstrap analysis supported the improvement trend of the final ensemble on the primary split. However, repeated patient split testing showed that the improvement is patient dependent. This is reported honestly as a limitation of the project.

## Output Files

The notebook generates result files such as:

```text
final_model_comparison.csv
main_ablation_table.csv
patient_wise_final_results.csv
bootstrap_summary.csv
repeated_patient_split_summary.csv
repeated_patient_split_results.csv
fusion_improvement_by_split.csv
final_project_summary.json
```

The notebook also generates figures such as the following:

```text
class_distribution.png
graph_example_non_seizure.png
graph_example_seizure.png
main_method_comparison_f1.png
main_method_comparison_fpr.png
confusion_matrix_final_model.png
roc_curve_final_model.png
pca_test_graph_embeddings.png
```

## Report and Poster

The final project report was written using the provided LaTeX template. The report includes:

* Abstract
* Introduction
* Related Work
* Data Description
* Methods
* Experiments and Results
* Conclusion
* References

The presentation poster summarizes the motivation, contribution, methodology, results, and conclusion of the project.

## Reproducibility

To reproduce the project, run the final notebook in Google Colab from the first cell to the last cell. The notebook was designed to run as a complete pipeline without manual changes after execution starts.

Because neural network training can involve random initialization, small differences in results may occur between runs. Random seeds are used where possible to reduce variation.

## Short Project Summary

This project proposes a patient-calibrated dynamic graph ensemble for cross-patient EEG seizure detection, where EEG windows are represented as brain connectivity graphs and validation-tuned fusion improves the main test F1 score while reducing false positives compared with the strongest individual graph baseline.
