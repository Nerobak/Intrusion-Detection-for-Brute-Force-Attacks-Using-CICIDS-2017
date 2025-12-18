Introduction (Markdown cell)

Cyberattacks such as brute-force login attempts remain a common threat to enterprise networks. Traditional signature-based intrusion detection systems often struggle to detect evolving or large-scale attacks. Machine learning offers an alternative by learning patterns from network traffic data and identifying malicious behavior automatically.

In this project, machine learning techniques are applied to network flow data from the CICIDS 2017 dataset to detect brute-force attacks. The goal is to distinguish benign network traffic from malicious brute-force activity using supervised classification models and evaluate their effectiveness.

Dataset Description (Markdown cell)

The dataset used in this project is CICIDS 2017, a publicly available intrusion detection dataset created by the Canadian Institute for Cybersecurity.

Dataset characteristics:

Flow-based network traffic features

Realistic benign and attack traffic

78 numerical features per flow

Includes brute-force attacks such as:

FTP-Patator

SSH-Patator

Source:
https://www.unb.ca/cic/datasets/ids-2017.html

For this project, the following subsets were used:

Benign-Monday-no-metadata.parquet

Bruteforce-Tuesday-no-metadata.parquet

Methodology (Markdown cell)

The project followed these steps:

Data Acquisition
The CICIDS 2017 dataset was downloaded using KaggleHub and loaded in Parquet format.

Data Preparation
Benign and brute-force traffic were combined into a single dataset. Infinite and missing values were removed to ensure data quality.

Label Engineering
A binary classification task was created:

0 → Benign traffic

1 → Brute-force attack traffic

Feature Scaling and Splitting
The dataset was split into training and testing sets (80/20 split) and standardized using StandardScaler.

Model Training
Two models were trained:

Random Forest Classifier

Linear SVM-style model using SGDClassifier

Evaluation
Models were evaluated using accuracy, precision, recall, F1-score, confusion matrices, and ROC-AUC.

Tools
- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib

Results (Markdown cell)

The Random Forest classifier achieved near-perfect performance in detecting brute-force attacks. The confusion matrix shows very few misclassifications, and the ROC-AUC score indicates excellent separation between benign and malicious traffic.

The linear SVM-style model also performed well, though Random Forest consistently achieved higher recall and overall accuracy.

These results demonstrate that machine learning models can effectively detect brute-force attacks in network traffic using flow-based features.

Conclusion (Markdown cell)

This project demonstrated the effectiveness of machine learning for intrusion detection using the CICIDS 2017 dataset. By analyzing network flow features, the trained models were able to accurately distinguish between benign traffic and brute-force attack traffic.

The Random Forest model performed exceptionally well, making it a strong candidate for practical intrusion detection systems. While SVM-based models are effective, their computational cost makes tree-based models more suitable for large-scale network datasets.

Limitations and Future Work (Markdown cell)

Limitations:

The dataset is highly imbalanced, which may inflate accuracy metrics.

Only brute-force attacks were considered.

Models were trained offline rather than in real time.

Future Work:

Include additional attack types such as botnets and DDoS

Apply deep learning models (e.g., LSTM for time-series flows)

Perform feature selection to reduce dimensionality

Deploy the model in a real-time IDS or SIEM environment

Results
The Random Forest model achieved near-perfect performance in detecting brute-force attacks, demonstrating the effectiveness of ML-based intrusion detection.
