# IoT IDS Evasion Attacks

This repository contains the IDS models, preprocessing pipeline, dataset samples, and adversarial evasion attacks developed for the project **“Investigating Evasion Attacks on AI-Driven Intrusion Detection Systems in IoT Environments.”**  
The project evaluates the robustness of machine learning and deep learning-based Intrusion Detection Systems (IDS) when exposed to adversarial manipulation within IoT environments. Multiple models and attack methodologies were implemented to measure misclassification behavior, Attack Success Rate (ASR), and overall resilience.

---

## Dataset Information

### Primary Dataset: CIC IoT-DIAD 2024  
All experiments in this project are based on the **CIC IoT-DIAD 2024 dataset**, provided by the Canadian Institute for Cybersecurity (CIC).  
Dataset link: https://www.unb.ca/cic/datasets/iot-diad-2024.html  

This dataset offers flow-level IoT traffic containing both benign behavior and a wide variety of cyberattacks across multiple IoT devices. It provides 83 statistical network features per flow and is widely used for research on intrusion detection and IoT security.

### Stratified Sample Used in This Repository  
A stratified dataset sample, **`sample_stratified_250k_ready.csv`**, is included in the repository to enable reproducible experimentation and reduce computational overhead.

**Sample Characteristics:**  
- Total samples: approximately 250,000 flows  
- Original features: 83  
- Features after preprocessing: 73  
- Contains 14 attack categories + benign flows  
- Flow-level tabular IoT telemetry extracted from CIC IoT-DIAD 2024  

**Preprocessing Performed:**  
- Removal of identifiers (Flow ID, IP addresses, timestamps)  
- Removal of redundant or highly correlated features  
- Verification of zero missing values across all numerical attributes  
- Duplicate detection using more than 70 flow characteristics (only six exact duplicates removed)  
- Outliers preserved to maintain real-world attack behavior patterns  

This stratified sample was used for training all IDS models and performing adversarial attacks (FGSM, PGD, Boundary, Hybrid, Surrogate-guided).

---

## IDS Models Implemented
- Random Forest (RF)  
- XGBoost  
- 1D-Convolutional Neural Network (1D-CNN)  
- Long Short-Term Memory Network (LSTM)

Models were trained using IoT tabular traffic samples and evaluated on both clean and adversarial inputs.

---

## Adversarial Attack Methods

### 1- Fast Gradient Sign Method (FGSM)
Implemented based on:  
**Sorensen et al., “Adversarial Evasion Attacks on OCC-Based Machine Learning Intrusion Detection Systems in the Internet of Things,” SATC 2025.**

---

### 2- Projected Gradient Descent (PGD)
Adopted as an iterative extension of FGSM using the foundational framework described by:  
**Sorensen et al., SATC 2025.**

PGD was additionally applied to non-differentiable models using surrogate-guided attacks.

---

### 3- Boundary Attack (Black-Box, Decision-Based)
Implemented following:  
**Kazoom et al., “Boundary on the Table: Efficient Black-Box Decision-Based Attacks for Structured Data,” 2025.**

---

### 4- Hybrid Evolutionary Attack (SIGMA-Like)
Inspired by the metaheuristic adversarial generation approach:  
**Msika et al., “SIGMA: Strengthening IDS with GAN and Metaheuristics Attacks,” 2019.**

A computationally efficient hybrid variant was developed using mutation, selection, and local-search operators.

---

### 5- Surrogate-Guided Attacks for Black-Box Models
To enable gradient-based attacks on non-differentiable models, an MLP surrogate was trained to approximate the target classifier, following:  
**Asimopoulos et al., “Surrogate-Guided Adversarial Attacks: Enabling White-Box Methods in Black-Box Scenarios,” 2024.**

---

### 6- Additional FGSM/Black-Box Reference
General IDS adversarial evaluation and FGSM usage informed by:  
**Barik & Misra, “IDS-Anta: An Open-Source Code with a Defense Mechanism to Detect Adversarial Attacks for Intrusion Detection Systems,” Software Impacts 2024.**

---

## Repository Structure
`/models` → Trained IDS models  
`/EDA-Samples` → Dataset samples for training and adversarial attacks  
`/attacks` → FGSM, PGD, Boundary, and Hybrid attack implementations  
`/evaluation` → ASR calculations, confusion matrices, metrics  

---

## Project Objectives
- Assess adversarial robustness of classical and deep IDS models  
- Compare white-box, black-box, and surrogate-guided attack performance  
- Quantify ASR, accuracy degradation, and feature sensitivity  
- Provide reproducible pipelines for IoT adversarial security research  

---

## How to Use
1. Install project dependencies  
2. Load dataset samples and preprocess them  
3. Train an IDS model or load pre-trained models  
4. Execute an adversarial attack script of choice  
5. Review evaluation outputs in `/evaluation`  

---

## References
1. Sorensen, D. L., Baza, M., Badr, M. M., & Salman, T. (2025).  
2. Kazoom, R., Ratzabi, Y., Rothstein, E., & Hadar, O. (2025).  
3. Msika, S., Quintero, A., & Khomh, F. (2019).  
4. Asimopoulos, D. C., et al. (2024).  
5. Barik, K., & Misra, S. (2024).  

---

## License
Distributed under the MIT License.
