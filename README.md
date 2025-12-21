Brute-Force Attack Detection with Machine Learning (CICIDS 2017)

Brute-force login attempts continue to be a common attack technique against enterprise networks. While traditional signature-based intrusion detection systems are effective for known patterns, they often struggle to detect large-scale or evolving attacks.
This project explores the use of supervised machine learning to detect brute-force activity in network traffic. Using flow-based features from the CICIDS 2017 dataset, the goal is to distinguish benign traffic from brute-force attacks targeting FTP and SSH services.
________________________________________

Table of Contents

1.	Project Overview
2.	Dataset
3.	Methodology
4.	Models
5.	Results
6.	How to Run
7.	Limitations
8.	Future Work
9.	Tools
10.	References
________________________________________

Project Overview

The objective of this project is to build a binary classification model capable of identifying brute-force network traffic and separating it from normal activity.
Traffic labels used in this project:

0 — Normal (benign) network traffic

1 — Brute-force attack traffic related to FTP or SSH services
________________________________________

Dataset

The dataset used is CICIDS 2017, created by the Canadian Institute for Cybersecurity at the University of New Brunswick.
Key characteristics of the dataset include:

•	Flow-based network traffic represented as numerical features

•	Realistic mixes of benign and malicious activity

•	Approximately 78 features per network flow, depending on the export

•	Inclusion of brute-force attacks such as FTP-Patator and SSH-Patator

For this project, the following subsets were used:

•	Benign-Monday-no-metadata.parquet

•	Bruteforce-Tuesday-no-metadata.parquet
________________________________________

Methodology

The project followed a standard machine learning workflow.
First, the CICIDS 2017 data was obtained using KaggleHub or manual download and loaded from Parquet files.
Next, benign and brute-force traffic were combined into a single dataset. Infinite values were replaced with missing values, and rows containing missing data were removed to create a clean baseline for model training.
Labels were then engineered for binary classification. Benign traffic was mapped to class 0, while all brute-force traffic related to FTP-Patator and SSH-Patator was mapped to class 1.
The dataset was split into training and testing sets using an 80/20 split, with stratification applied to preserve class distribution. Feature scaling was performed using StandardScaler, which is especially important for linear models.
Finally, models were trained and evaluated using accuracy, precision, recall, F1-score, confusion matrices, and ROC-AUC.
________________________________________

Models

Two supervised classification models were used in this project.
The first model was a Random Forest classifier. This model was chosen because it performs well on tabular data, captures non-linear relationships, and is robust to noisy features. Class balancing was applied to reduce the impact of dataset imbalance.
The second model was a linear SVM-style classifier implemented using SGDClassifier. This model provides fast training on large datasets and serves as a strong linear baseline. Feature scaling and class balancing were both required for optimal performance.
________________________________________

Results

The Random Forest model achieved near-perfect performance in detecting brute-force attacks. The confusion matrix showed very few misclassifications, and the ROC-AUC score indicated excellent separation between benign and malicious traffic.
The linear SVM-style model also performed well, but it generally achieved lower recall and overall accuracy compared to the Random Forest classifier.
These results demonstrate that machine learning models can effectively identify brute-force attacks using flow-based network features.
________________________________________

How to Run

Install the required dependencies:
pip install pandas numpy scikit-learn matplotlib pyarrow
Open the Jupyter notebook named BruteForceDetection_updated.ipynb.
In the notebook, update the dataset directory path so it points to the folder containing the CICIDS 2017 Parquet files:
DATA_DIR = Path(r"C:\path\to\cicids2017")
Ensure the directory includes the following files:
•	Benign-Monday-no-metadata.parquet
•	Bruteforce-Tuesday-no-metadata.parquet
Run the notebook cells from top to bottom.
________________________________________

Limitations

The dataset is imbalanced, which can cause accuracy to appear inflated. Metrics such as recall, F1-score, and ROC-AUC provide a more reliable evaluation.
Only brute-force attacks were included in this project, limiting the scope of detection.
All models were trained offline and were not evaluated in a real-time detection environment.
________________________________________

Future Work

Future improvements could include incorporating additional attack types such as botnets or DDoS attacks.
Deep learning approaches, such as LSTM models, could be explored to capture temporal behavior in network flows.
Feature selection or dimensionality reduction techniques could be applied to reduce model complexity.
The model could also be deployed as part of a real-time IDS or SIEM pipeline using streaming network data.
________________________________________

Tools

Python
Pandas and NumPy
Scikit-learn
Matplotlib
________________________________________

References

CICIDS 2017 Dataset, Canadian Institute for Cybersecurity
https://www.unb.ca/cic/datasets/ids-2017.html


The Random Forest model achieved near-perfect performance in detecting brute-force attacks, demonstrating the effectiveness of ML-based intrusion detection.
