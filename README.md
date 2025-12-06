# IoT IDS Evasion Attacks

This repository contains the IDS models, preprocessing pipeline, dataset samples, and adversarial evasion attacks developed for the project **“Investigating Evasion Attacks on AI-Driven Intrusion Detection Systems in IoT Environments.”**  
The project evaluates the robustness of machine learning and deep learning-based Intrusion Detection Systems (IDS) when exposed to adversarial manipulation within IoT environments. Multiple models and attack methodologies were implemented to measure misclassification behavior, Attack Success Rate (ASR), and overall resilience.

---

##  IDS Models Implemented
- Random Forest (RF)  
- XGBoost  
- 1D-Convolutional Neural Network (1D-CNN)  
- Long Short-Term Memory Network (LSTM)

Models were trained using IoT tabular traffic samples and evaluated on both clean and adversarial inputs.

---

##  Adversarial Attack Methods

### 1- Fast Gradient Sign Method (FGSM)
Implemented based on:  
**Sorensen et al., “Adversarial Evasion Attacks on OCC-Based Machine Learning Intrusion Detection Systems in the Internet of Things,” SATC 2025.**

---

### 2- Projected Gradient Descent (PGD)
Adopted as an iterative extension of FGSM using the same foundational framework described by:  
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

A computationally efficient hybrid version was developed using mutation, selection, and local-search operators.

---

### 5- Surrogate-Guided Attacks for Black-Box Models
To enable gradient-based attacks on non-differentiable models, an MLP surrogate was trained to approximate the target classifier, following:  
**Asimopoulos et al., “Surrogate-Guided Adversarial Attacks: Enabling White-Box Methods in Black-Box Scenarios,” 2024.**

---

### 6- Additional FGSM/Black-Box Reference
General IDS adversarial evaluation and FGSM usage informed by:  
**Barik & Misra, “IDS-Anta: An Open-Source Code with a Defense Mechanism to Detect Adversarial Attacks for Intrusion Detection Systems,” Software Impacts 2024.**

---

##  Repository Structure
`/models` → Trained IDS models

`/samples` → Dataset samples for training & attacks

`/attacks` → FGSM, PGD, Boundary, Hybrid on the madles

`/evaluation` → ASR calculations, confusion matrices, metrics


---

##  Project Objectives
- Assess adversarial robustness of classical and deep IDS models  
- Compare white-box, black-box, and surrogate-guided attack performance  
- Quantify ASR, accuracy degradation, and feature sensitivity  
- Provide reproducible pipelines for IoT adversarial security research  

---

##  How to Use
1. Install project dependencies  
2. Load dataset samples and preprocess them  
3. Train an IDS model or load pre-trained models  
4. Execute an adversarial attack script of choice  
5. Review evaluation outputs in `/evaluation`  

---

##  References
1. Sorensen, D. L., Baza, M., Badr, M. M., & Salman, T. (2025).  
2. Kazoom, R., Ratzabi, Y., Rothstein, E., & Hadar, O. (2025).  
3. Msika, S., Quintero, A., & Khomh, F. (2019).  
4. Asimopoulos, D. C., et al. (2024).  
5. Barik, K., & Misra, S. (2024).  

---

##  License
Distributed under the **MIT License**.
