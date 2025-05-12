# 🔐 Threat Modeling Guide for AI/ML/DL Systems

![Day 1- 20 Recap](images/day1-20-poster.png)

Here’s a structured threat modeling guide for **AI/ML/DL systems** based on the core concepts we have talked in past 20 Days. This is broken down to align with pedagogical clarity and real-world security impact.

---

## I. 📊 Learning Paradigms (Supervised vs. Unsupervised Learning)

| Concept                   | Threat Vectors                                                 | Threat Description                                                                   | Impact                                        | Mitigation                                                      |
| ------------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------ | --------------------------------------------- | --------------------------------------------------------------- |
| **Supervised Learning**   | - Data poisoning<br>- Label flipping<br>- Membership inference | Attacker manipulates labels to bias model behavior. Infer if specific data was used. | Model misclassification<br>Privacy breach     | Data validation<br>Robust training<br>DP (Differential Privacy) |
| **Unsupervised Learning** | - Outlier injection<br>- Cluster boundary manipulation         | Inject anomalous data to corrupt clustering/grouping.                                | Poor clustering<br>Faulty feature engineering | Anomaly detection<br>Noise-tolerant algorithms                  |

---

## II. 📈 Problem Type (Regression vs. Classification)

| Type               | Threat Vectors                                  | Threat Description                                                | Impact                                 | Mitigation                                                         |
| ------------------ | ----------------------------------------------- | ----------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------------ |
| **Regression**     | - Output manipulation<br>- Adversarial outliers | Inject values that skew the curve drastically.                    | Bad predictions in finance/forecasting | Robust statistics<br>Outlier detection                             |
| **Classification** | - Evasion attacks<br>- Model inversion          | Modify input to shift to a wrong class. Extract features via API. | Fraud evasion<br>PII leakage           | Adversarial training<br>API rate limiting<br>Confidence thresholds |

---

## III. 🧠 Model Concepts

| Concept                                | Threat Vectors                                            | Threat Description                                          | Impact                                  | Mitigation                                                    |
| -------------------------------------- | --------------------------------------------------------- | ----------------------------------------------------------- | --------------------------------------- | ------------------------------------------------------------- |
| **Overfitting**                        | - Model memorizes sensitive data<br>- Poor generalization | Attacker recovers training data or causes high test error   | Privacy loss<br>Performance degradation | Regularization<br>Cross-validation                            |
| **Decision Trees**                     | - Path probing<br>- Rule extraction                       | Reveal logic via output observation                         | IP theft<br>Gaming the model            | Ensemble methods<br>Access control                            |
| **Boosting (e.g., XGBoost, AdaBoost)** | - Cascade poisoning                                       | Poison early weak learners to propagate error               | Biased final model                      | Early stopping<br>Data sanitization                           |
| **Loss Functions**                     | - Gradient manipulation<br>- Label flipping               | Craft data to drive optimizer to suboptimal minima          | Inaccurate predictions                  | Robust loss functions (e.g., MAE over MSE)                    |
| **Gradient Descent**                   | - Adversarial gradients<br>- Model extraction             | Steer model via poisoned gradients                          | Backdoors<br>Loss of confidentiality    | DP-SGD<br>Gradient clipping                                   |
| **Neural Networks**                    | - Adversarial examples<br>- Backdoors<br>- Trojans        | Minor perturbations trick model; implant malicious behavior | Model unreliability<br>Trust violation  | Adversarial training<br>Activation analysis<br>Neuron pruning |

---

## IV. 🧪 Training & Feature Engineering

| Concept                                         | Threat Vectors                                            | Threat Description                                           | Impact                                          | Mitigation                                              |
| ----------------------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | ------------------------------------------------------- |
| **Feature Engineering**                         | - Feature poisoning<br>- Feature leakage                  | Craft features to mislead the model; leak sensitive features | Model skew<br>Privacy violations                | Feature selection audit<br>Leakage checks               |
| **Dimensionality Reduction (e.g., PCA, t-SNE)** | - Component injection<br>- Visualization deception        | Add noisy directions to alter embedding                      | False data interpretation<br>Attack obfuscation | Robust PCA<br>Manual component review                   |
| **Training Data Pipeline**                      | - Data poisoning<br>- Supply chain attacks                | Replace or corrupt data at ingestion stage                   | Compromised training                            | Versioning<br>Hash validation<br>Secure pipeline        |
| **Label Generation**                            | - Crowdsourcing manipulation<br>- Scripted label flipping | Skewed labels via malicious labelers                         | Garbage-in-garbage-out                          | Active learning<br>Quality control<br>Human-in-the-loop |

---

## V. ⚙️ Attack Techniques Across Lifecycle

| Phase                 | Threat Type                               | Example                                          | Mitigation                                       |
| --------------------- | ----------------------------------------- | ------------------------------------------------ | ------------------------------------------------ |
| **Data Collection**   | Poisoning / Privacy attacks               | Malicious contributors to training set           | Provenance tracking<br>DP                        |
| **Model Training**    | Gradient-based attacks                    | Introduce poisoned gradients                     | DP-SGD<br>Gradient clipping                      |
| **Model Inference**   | Adversarial inputs / Membership inference | Perturbed images to evade detection              | Confidence thresholds<br>Noise-tolerant training |
| **Model Deployment**  | Model extraction / API abuse              | Black-box API probing                            | Rate limiting<br>Access controls                 |
| **Model Maintenance** | Concept drift exploitation                | Gradual poisoning of continuously trained models | Drift detection<br>Human audit                   |

---

## VI. 📦 Advanced Considerations

| Area                                  | Threat                             | Example                                    | Countermeasure                                  |
| ------------------------------------- | ---------------------------------- | ------------------------------------------ | ----------------------------------------------- |
| **Model Explainability (SHAP, LIME)** | Model stealing via explanations    | Output interpretation helps recreate model | Limit granularity<br>Explainability abstraction |
| **AutoML**                            | Auto-poisoning                     | Exploiting the automation loop             | Human verification<br>Dataset whitelisting      |
| **Transfer Learning**                 | Pretrained model backdoors         | Pretrained on poisoned corpora             | Re-train last layers<br>Audit source            |
| **Federated Learning**                | Malicious clients<br>Model leakage | Poisoned local updates                     | Secure aggregation<br>Client vetting            |

---

## VII. 🔍 Prioritized Risk Assessment (STRIDE-Like)

| Threat Type                | Examples in ML Context                    | Security Property Violated |
| -------------------------- | ----------------------------------------- | -------------------------- |
| **Spoofing**               | Fake clients in federated learning        | Authentication             |
| **Tampering**              | Data poisoning, gradient manipulation     | Integrity                  |
| **Repudiation**            | Malicious labeling with no accountability | Non-repudiation            |
| **Information Disclosure** | Membership inference, model inversion     | Confidentiality            |
| **Denial of Service**      | Flooding API with adversarial inputs      | Availability               |
| **Elevation of Privilege** | Exploiting AutoML or deployment pipelines | Authorization              |

---
![Day 1-20 Recap](images/Impact Mapping.jpg)
