# Adversarial Attack Methods Implemented

This project implements four adversarial evasion attacks adapted from peer-reviewed research.  
Each method was selected based on its relevance, strength, and applicability to Intrusion Detection Systems (IDS) operating in IoT environments.  
The IDS literature consistently demonstrates that both gradient-based and gradient-free attacks expose severe vulnerabilities in ML-driven security systems.  
Accordingly, we implemented complementary attack categories: **white-box**, **black-box**, and **metaheuristic** evasion methods.

---

## 1. Fast Gradient Sign Method (FGSM)

**Reference Basis:**  
- *FGSM-FOR-IDS*  
- *Adversarial Evasion Attacks on OCC-Based ML IDS in IoT (SATC 2025)*  

**Description:**  
FGSM is a single-step gradient attack that perturbs the input in the direction that most increases the model’s loss. It is widely used in IDS research as a baseline adversarial method.

**Why This Attack Was Used:**  
- It is the simplest yet most widely adopted adversarial method.  
- It provides a controlled, interpretable baseline for evaluating vulnerability.  
- Fast to compute for large-scale IoT datasets.  
- It is used across multiple IDS research papers, making results comparable.

**Why FGSM Is Strong:**  
- Even minimal perturbations can significantly degrade IDS performance.  
- Deep learning models (CNN/LSTM) are highly sensitive to linear gradient changes.  

**Mathematical Form:**  
\[
x_{\text{adv}} = x + \epsilon \cdot \text{sign}(\nabla_x J(\theta, x, y))
\]

---

## 2. Projected Gradient Descent (PGD)

**Reference Basis:**  
- *SATC 2025 OCC IDS attack model*  
- *Model Evasion Attack on IDS Using Adversarial Machine Learning*

**Description:**  
PGD is an iterative extension of FGSM. It repeatedly applies small gradient steps and projects the sample back into the allowed perturbation region.

**Why This Attack Was Used:**  
- Cited in the literature as the **most powerful first-order attack**.  
- Provides a rigorous evaluation of system robustness.  
- Allows testing model resilience under stronger and more realistic manipulations.  
- Works with surrogate models, allowing application to RF/XGBoost.

**Why PGD Is Strong:**  
- Iterative refinements provide significantly higher Attack Success Rates (ASR).  
- Has been shown in IDS studies to collapse classifier accuracy almost completely.

**Update Rule:**  
\[
x^{t+1} = \Pi_{\epsilon}(x^t + \alpha \cdot \text{sign}(\nabla_x J(x^t, y)))
\]

---

## 3. Boundary Attack (Black-Box, Decision-Based)

**Reference Basis:**  
- *Boundary on the Table: Efficient Black-Box Decision-Based Attacks for Structured Data (Kazoom et al., 2025)*

**Description:**  
A gradient-free attack that requires only model decisions (predicted labels).  
It uses feature ranking (via SHAP in the reference work) and binary search steps to move the sample toward the decision boundary.

**Why This Attack Was Used:**  
- Realistic for IoT environments where the attacker does not know internals of the IDS.  
- Works effectively for tree models and deep learning models alike.  
- Represents the **black-box attack scenario** required by many security standards.

**Why Boundary Attack Is Strong:**  
- Does not need gradients or probability outputs.  
- Extremely challenging for IDS to defend because the model cannot detect gradient direction.  
- Effective even on well-regularized models like XGBoost.

**Core Process:**  
1. Initialize from or move toward a misclassified point.  
2. Rank influential features.  
3. Apply directional perturbations toward the decision boundary.  
4. Compress perturbations via binary search.  

---

## 4. Hybrid Evolutionary Attack (Metaheuristic / Genetic)

**Reference Basis:**  
- *Model Evasion Attack on Intrusion Detection Systems Using Adversarial Machine Learning*

**Description:**  
A gradient-free attack using principles of evolutionary optimization.  
It mutates non-functional features, evaluates fitness based on misclassification probability, and selects best candidates across generations.

**Why This Attack Was Used:**  
- Gradient-free model needed for RF and XGBoost.  
- Captures non-linear interactions that gradient-based attacks miss.  
- Evaluates IDS robustness under **optimization-driven adversaries**, which are highly realistic in IoT botnet contexts.  
- Paper demonstrates strong evasion even under strict feature constraints.

**Why It Is Strong:**  
- Able to bypass models that do not expose gradients.  
- Can explore wide perturbation spaces not reachable by PGD/FGSM.  
- Maintains validity by modifying only non-functional features.

**Mechanism:**  
- Population initialization  
- Mutation of selected features  
- Selection based on misclassification probability  
- Iterative refinement until convergence  

---

# Summary of Attack Roles and Strengths

| Attack | Access Level | Strength | Why Included |
|--------|--------------|----------|--------------|
| **FGSM** | White-box | Fast, high baseline impact | Standard IDS benchmark; measures gradient sensitivity |
| **PGD** | White-box (iterative) | Strongest first-order attack | Tests worst-case vulnerability; used in literature as the main adversarial baseline |
| **Boundary** | Black-box, labels only | Realistic attacker model | Works on non-differentiable models; strong for structured tabular data |
| **Hybrid Evolutionary** | Gradient-free | Optimization-driven bypass | Designed for tree models; replicates attacker search behavior |

---

# Why We Selected These Attacks for the Project

The four attacks together provide **comprehensive evasion coverage**:

- **FGSM + PGD** evaluate how gradient-sensitive the IDS is.  
- **Boundary Attack** assesses robustness in realistic black-box deployments.  
- **Hybrid Evolutionary Attack** evaluates non-differentiable, ensemble-based IDS models.  

This aligns with the referenced research, which highlights that IoT IDS systems must be tested under **multiple adversarial threat models** to accurately measure robustness.

