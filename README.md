# Adversarial Attack Methods Implemented

This project implements four major evasion attacks derived exclusively from the referenced research papers.  
Each attack was adapted to tabular IoT network traffic and evaluated on classical and deep learning IDS models.

---

## 1. Fast Gradient Sign Method (FGSM)

**Reference basis:**  
- FGSM-FOR-IDS  
- *Adversarial Evasion Attacks on OCC-Based ML IDS in IoT (SATC 2025)*  

FGSM is a white-box, single-step gradient-based attack that perturbs each feature in the direction that maximizes the model loss.  
The referenced works demonstrate that IoT IDS systems are highly sensitive to small linear perturbations.

**Formulation:**
\[
x_{\text{adv}} = x + \epsilon \cdot \text{sign}(\nabla_x J(\theta, x, y))
\]

**Key points:**
- Very fast to compute  
- Causes significant drops in accuracy for deep models  
- Used as a baseline attack  
- Applied directly to differentiable models and via surrogate for RF/XGBoost  

---

## 2. Projected Gradient Descent (PGD)

**Reference basis:**  
- SATC 2025 OCC attack paper  
- *Model Evasion Attack on IDS using Adversarial Machine Learning*

PGD extends FGSM by applying multiple iterative perturbations while projecting back into the allowed perturbation region.  
The cited papers report PGD as the most effective gradient-based attack for IDS systems, frequently yielding near-complete evasion.

**Update rule:**
\[
x^{t+1} = \Pi_{\epsilon}(x^t + \alpha \cdot \text{sign}(\nabla_x J(x^t, y)))
\]

**Key points:**
- Stronger and more realistic than FGSM  
- Achieves high ASR across IoT datasets  
- Can collapse model performance under white-box assumptions  
- Surrogate-guided version used for RF/XGBoost  

---

## 3. Boundary Attack (Black-Box, Decision-Based)

**Reference basis:**  
- *Boundary on the Table: Efficient Black-Box Decision-Based Attacks for Structured Data (Kazoom et al., 2025)*

This attack requires only **class labels**, not gradients or probabilities.  
The referenced work proposes a SHAP-guided decision-based boundary exploration specifically for tabular structures, making it ideal for IoT traffic data.

**Core steps from the paper:**
1. Start from a misclassified sample or move toward the boundary  
2. Use SHAP to rank sensitive features  
3. Apply iterative perturbation toward the decision boundary  
4. Use binary search to minimize perturbation magnitude  

**Key points:**
- Completely black-box  
- Effective for tree models and deep models  
- Mimics realistic attacker capabilities in IoT environments  

---

## 4. Hybrid Evolutionary Attack (Metaheuristic / Genetic)

**Reference basis:**  
- *Model Evasion Attack on Intrusion Detection Systems using Adversarial Machine Learning*

This attack uses evolutionary optimization to generate adversarial examples without requiring gradients.  
It is particularly effective for non-differentiable models like Random Forest and XGBoost.

**Mechanism:**
- Population initialization  
- Mutation of non-functional features  
- Selection based on misclassification probability  
- Iterative improvement across generations  

**Key points:**
- Gradient-free  
- Effective for black-box or hard-to-differentiate models  
- Preserves functional (behavioral) feature constraints  
- Reduced population size and generations used for computational efficiency  

---

# Summary Table

| Attack Method | Access Required | Type | Why Included |
|---------------|----------------|------|--------------|
| FGSM | Gradients | White-box | Fast baseline attack used in IDS literature |
| PGD | Gradients | White-box (strong) | High ASR; strongest iterative gradient attack |
| Boundary | Labels only | Black-box | Realistic IoT threat scenario; SHAP-guided |
| Hybrid Evolutionary | No gradients | Evolutionary / Metaheuristic | Effective on RF/XGBoost and gradient-free models |

All attack implementations are directly grounded in the referenced academic papers and adapted for tabular IoT traffic.
