## Academic Basis for the Evaluation Module

The evaluation framework implemented in this project is grounded in the metrics, analysis methods, and adversarial success criteria discussed across the following three research studies:

- *Enhancing IDS Performance Through a Comparative Analysis of Random Forest, XGBoost, and Deep Neural Networks* (2023)  
- *Mitigating Adversarial and AI-Evasion Attacks in Cybersecurity: Challenges and Strategies* (2023)  
- *Model Evasion Attack on Intrusion Detection Systems Using Adversarial Machine Learning* (2020)

Although each study approaches IDS robustness from a different technical perspective, they collectively establish a consistent set of evaluation metrics and evasion-success indicators that our unified module operationalizes.

### 1. Core Performance Metrics

Across the three references, the following metrics serve as the primary indicators of IDS classification quality:

- **Accuracy** – Measures overall correctness.  
- **Precision** – Indicates the reliability of positive (attack) predictions.  
- **Recall** – Reflects the IDS’s ability to detect all actual attack samples.  
- **F1-score** – A balanced harmonic mean of precision and recall, used extensively when traffic is imbalanced.  

These metrics form the baseline for comparing clean vs. adversarial performance.

### 2. Inclusion of AUC for Normal vs. Attack Separation

Both adversarial-attack and IDS-benchmarking literature highlight **AUC** as a valuable metric for assessing whether adversarial samples cause malicious traffic to gain higher “Benign” probability.

Our module therefore supports:
- **Clean AUC**
- **Adversarial AUC**
- **AUC shift**, used as an indicator of the model’s vulnerability to evasion.

This aligns with the treatment of ROC-based evaluation discussed in the mitigation and robustness paper.

### 3. Attack-Specific Metrics (ASR)

Following the adversarial-machine-learning study, our evaluation module incorporates:

- **Attack Success Rate (ASR)**  
  Defined as the proportion of adversarial samples whose predicted class changes in a direction favorable to evasion (e.g., Attack → Benign).

ASR is a central, explicit measure of evasion effectiveness in the literature and provides a direct quantification of how severe the performance degradation is.

### 4. Clean vs. Adversarial Comparison Framework

All three references emphasize *comparative evaluation*, not isolated metric reporting.  
To match this methodology, the module computes:

- Metric tables for both conditions  
- Delta-drop analysis (Clean − Adversarial)  
- Side-by-side confusion matrices  
- Class-level performance degradation  

This reflects academic practice in assessing adversarial robustness by measuring not only accuracy loss but also structural changes in error distribution.

### 5. Confusion Matrix Interpretation

Prior studies show that misclassification patterns—not only aggregated metrics—are essential to understanding attack behavior.  
Therefore, the module automatically generates:

- A normalized clean confusion matrix  
- A normalized adversarial confusion matrix  

allowing visual inspection of how traffic distribution shifts under attack pressure.

### 6. Justification for the Unified Evaluation Design

The evaluation functions implemented here were designed to satisfy three academic requirements drawn directly from the referenced papers:

1. **Performance Stability Analysis**  
   – As used in IDS benchmark studies.  
2. **Adversarial Impact Quantification**  
   – Emphasized in evasion-attack research.  
3. **Detection-Capability Degradation Measurement**  
   – Discussed in cybersecurity mitigation literature.

Our module integrates these ideas into one standardized pipeline that computes:

- Clean vs. adversarial accuracy  
- Weighted precision, recall, and F1  
- AUC shifts  
- ASR  
- Per-class scoring  
- Confusion matrix deviation  
- Visual performance comparison  
- Optional exportable artifacts (CSV, Excel, JSON, PNG)

This ensures the evaluation results produced in the project are academically interpretable and consistent with published methodologies.

### 7. Summary

These three references collectively define the theoretical foundation for evaluating IDS robustness under adversarial settings.  
The evaluation module used in this repository is therefore a direct operationalization of the metrics and criteria consistently applied in these studies, allowing reliable, academically defensible assessment of evasion attacks against IoT-focused IDS models.
