# IDS Models Used in This Project

This project evaluates the robustness of four different Intrusion Detection System (IDS) models commonly used in IoT cybersecurity research. The selected models represent a diverse range of machine learning and deep learning paradigms, enabling a comprehensive assessment of how different architectures respond to adversarial evasion attacks.

---

## 1. Random Forest (RF)

Random Forest is an ensemble learning model built from multiple decision trees.  
Each tree votes on the predicted class, and the forest aggregates these votes to produce the final output.

### Why RF Was Used
- Strong performance on tabular IoT network traffic.
- Naturally robust against noise and overfitting.
- Fast training and prediction speeds.
- Frequently used in IDS literature as a classical baseline.

### Strengths
- Handles high-dimensional and imbalanced data efficiently.
- Captures nonlinear decision boundaries.
- Resistant to variance due to ensemble averaging.

### Weakness Under Adversarial Attacks
- Lacks gradient information → requires black-box or surrogate-guided attacks.
- Vulnerable to evasion methods that push samples across shallow decision thresholds.

---

## 2. XGBoost

XGBoost (Extreme Gradient Boosting) is a boosting ensemble algorithm that builds sequential trees, where each tree corrects errors from previous ones.

### Why XGBoost Was Used
- Known for state-of-the-art performance on structured/tabular data.
- Outperforms many classical ML methods in IDS benchmarks.
- Highly optimized and capable of capturing subtle attack patterns.

### Strengths
- High accuracy due to gradient-boosting optimization.
- Handles feature interactions better than RF.
- Strong generalization on heterogeneous IoT traffic.

### Weakness Under Adversarial Attacks
- Non-differentiable → requires a surrogate model to generate gradient-based attacks (e.g., PGD).
- Decision boundaries can still be manipulated with carefully crafted perturbations.

---

## 3. 1D Convolutional Neural Network (1D-CNN)

1D-CNNs apply convolutional filters across sequential input features, making them suitable for IDS tasks where flows behave like ordered feature sequences.

### Why 1D-CNN Was Used
- CNNs extract local patterns and temporal-like feature relationships.
- Frequently used in network intrusion detection research.
- Performs well on large, structured IoT datasets.

### Strengths
- Learns hierarchical feature representations automatically.
- Captures spatial correlations between features.
- Supports gradient-based adversarial attacks directly (FGSM, PGD).

### Weakness Under Adversarial Attacks
- Highly sensitive to gradient-based perturbations (white-box attacks).
- Small changes in feature space can drastically shift predictions.

---

## 4. Long Short-Term Memory Network (LSTM)

LSTMs are recurrent neural networks capable of learning long-term dependencies.  
Although IoT flow data is not sequential in time, LSTMs are widely used in IDS research because of their ability to model complex feature interactions.

### Why LSTM Was Used
- Popular in IDS deep-learning literature.
- Learns implicit dependencies across network-flow features.
- Acts as a strong baseline for deep models.

### Strengths
- Good at modeling nonlinear relationships and long-range dependencies.
- Supports gradient-based white-box attacks easily.

### Weakness Under Adversarial Attacks
- Extremely sensitive to adversarial perturbations.
- Often exhibits high ASR in white-box scenarios.
- Decision boundaries are easily shifted by minimal noise.

---

# Summary of Model Selection Rationale

Using a combination of classical ML and deep learning architectures provides a complete adversarial evaluation landscape:

| Model Type | Examples | Purpose in This Project |
|------------|----------|------------------------|
| Classical ML | RF, XGBoost | Benchmark performance and assess black-box attack behavior |
| Deep Learning | 1D-CNN, LSTM | Evaluate white-box vulnerabilities under gradient-based attacks |

This diversity allows the study to:
- Compare susceptibility across model families  
- Measure the impact of FGSM, PGD, Boundary, and Hybrid attacks  
- Identify which architectures are more resilient for IoT IDS deployment  

Overall, this multi-model approach strengthens the validity and generalizability of the adversarial evaluation framework.

