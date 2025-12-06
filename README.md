## Stratified Sample Used in This Repository

A stratified dataset sample, **`sample_stratified_250k_ready.csv`**, is included in this repository to support reproducible, controlled, and computationally efficient experimentation. This sample was directly derived from the **CIC IoT-DIAD 2024** dataset and prepared using a multi-stage preprocessing and cleaning pipeline to ensure high data quality for intrusion detection and adversarial attack evaluation.

### Sample Composition and Statistics
- **Total Records:** Approximately 250,000 flow-based samples  
- **Original Features:** 83  
- **Features After Preprocessing:** 73  
- **Data Type:** Flow-level tabular network telemetry  
- **Included Classes:** Benign traffic + 14 IoT attack categories  
- **Attack Types Represented:**  
  - DoS SYN Flood  
  - DoS UDP Flood  
  - DDoS  
  - ICMP Flood  
  - ICMP Fragmentation  
  - Mirai  
  - DNS Spoofing  
  - SQL Injection  
  - XSS  
  - Brute Force  
  - Web-Based attacks  
  - Additional IoT-targeted attacks from the CIC IoT-DIAD 2024 dataset  

The sample preserves the natural imbalance found in IoT environments, where volumetric attacks such as DoS/DDoS dominate the traffic, while more complex attack categories appear in smaller volumes. This makes the sample highly representative of real-world IoT intrusion behavior.

### Preprocessing and Cleaning Procedures
The sample was subjected to an extensive preprocessing workflow to improve data quality and model compatibility:

1. **Removal of Identifier Columns**  
   Columns such as:
   - Flow ID  
   - Source/Destination IP  
   - Timestamps  
   - Internal dataset tracking fields  
   were removed because they do not provide meaningful learning value and may introduce bias.

2. **Feature Reduction and Deduplication**  
   - Redundant or highly correlated features were eliminated (e.g., Packet Length Mean, Flow Bytes/s).  
   - Duplicate flows were detected using more than **70 flow-level attributes**, ensuring strict duplicate removal.  
   - Only **six exact duplicates** were identified and removed, indicating high dataset integrity.

3. **Validation of Missing Values**  
   - All numerical columns were validated to contain **zero missing values** after cleaning.  
   - Ensures consistent model input and avoids unintended distortions in adversarial attack behavior.

4. **Retention of Relevant Outliers**  
   - Extreme values (e.g., high packet counts, long flow durations) were preserved because they reflect realistic attack behaviors, especially in DoS/DDoS contexts.

5. **Column Standardization**  
   - Final cleaned dataset maintains 73 informative features across flow statistics, timing, protocol behavior, flags, activity/idle metrics, and subflow information.

### Purpose of the Sample
This stratified sample is used throughout the repository for:

- **Training all IDS models** (RF, XGBoost, 1D-CNN, LSTM)  
- **Executing adversarial attacks**, including:  
  - FGSM  
  - PGD  
  - Boundary Attack  
  - Hybrid Evolutionary Attack  
  - Surrogate-based attacks  
- **Ensuring reproducible experimental conditions** across all models and attack methods  
- **Reducing computational cost** compared to the full CIC IoT-DIAD dataset (which contains millions of flows)  
- **Providing a standardized benchmark** for evaluating model robustness under adversarial conditions  

### Why This Sample Was Selected
- It maintains **real-world IoT traffic distributions**, including heavy attack dominance and diverse feature behavior.  
- It allows **efficient experimentation** on limited hardware while preserving statistical representativeness.  
- It ensures that all IDS models and attack methods operate on the **exact same input distribution**, enabling fair comparison.  
- It retains all important behavioral patterns (packet sizes, flow durations, idle/active times, protocol differences) necessary for model interpretability and adversarial sensitivity analysis.

This sample serves as the **central dataset** for the entire adversarial evaluation pipeline in this project.
