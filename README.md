# Generative-AI-for-Threat-Simulation-Bachelor-Thesis
Using CTGANs to simulate attack-like behavior in the form of tabular data in order to improve anomaly-based IDS robustness

## Overview

This repository contains the complete implementation and documentation for my Bachelor's Thesis.
The research addresses critical challenges in cybersecurity by leveraging Generative AI (GAI) to enhance the robustness of Anomaly-based Intrusion Detection Systems (AIDS). It combines Conditional Tabular GANs (CTGAN) for synthetic data generation with ChatGPT-4 for simulating advanced, obfuscated cyber attacks, creating a dynamic threat simulation framework.

## Research Objectives

1.  **Class Imbalance Mitigation:** Use CTGAN to improve detection of rare attack classes (R2L, U2R) in the imbalanced NSL-KDD dataset.
2.  **Adversarial Robustness:** Leverage ChatGPT-4 to simulate evasive attack variants that bypass traditional detection.
3.  **IDS Enhancement:** Determine if training on a synthetically-augmented dataset improves model resilience against novel threats.

## Technical Implementation

### Dataset
- **NSL-KDD:** Benchmark intrusion detection dataset with 41 features and 5 classes (`normal`, `DoS`, `Probe`, `R2L`, `U2R`).
- **Challenge:** Severe class imbalance (`R2L` and `U2R` attacks represent <1% of records).

### Methodology (CRISP-DM Framework)
1.  **Data Preprocessing:**
    - Mapped specific attacks to broad categories (`label_category`)
    - Created a binary label for anomaly detection (`label_binary`)
    - Encoded categorical features (`protocol_type`, `service`, `flag`)
    - Applied log-transformation to skewed numerical features

2.  **Synthetic Data Generation (CTGAN):**
    - Trained CTGAN on rare `R2L` and `U2R` classes
    - Generated 20,000 synthetic samples to balance the dataset
    - Created `synthetic_train_nsl_kdd` by combining synthetic and original data

3.  **Modeling:**
    - Built two **Random Forest** classifiers:
        - **Regular Model:** Trained on original, imbalanced data
        - **Synthetic Model:** Trained on CTGAN-augmented data
    - Used identical parameters (`n_estimators=100`, `random_state=42`)

4.  **Threat Simulation with ChatGPT-4:**
    - Extracted five rare attack records (3 R2L, 2 U2R) from test set
    - Used advanced prompt engineering to simulate obfuscation techniques:
        - Code Jumbling
        - Dead Code Insertion
        - Control Flow Obfuscation
        - Switch Method
        - Social Engineering
    - Injected obfuscated samples into both models

5.  **Evaluation:**
    - Evaluated on standard `kdd_test` set using Accuracy, Precision, Recall, F1-Score
    - Tested robustness against LLM-obfuscated attack samples


## Conclusion

- The **Regular model** performed better on the imbalanced test set, likely due to overfitting on dominant classes.
- The **Synthetic model** demonstrated supe
