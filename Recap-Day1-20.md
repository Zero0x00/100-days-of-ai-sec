# Day 1-20 Recap

![Day 1- 20 Recap](images/day1-20-poster.png)

Here’s a structured threat modeling guide for **AI/ML/DL systems** based on the core concepts we have talked in past 20 Days. This is broken down to align with pedagogical clarity and real-world security impact.

***

## I. 📊 Learning Paradigms (Supervised vs. Unsupervised Learning)

| Concept                   | Threat Vectors                                                        | Threat Description                                                                   | Impact                                               | Mitigation                                                             |
| ------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------- | ---------------------------------------------------------------------- |
| **Supervised Learning**   | <p>- Data poisoning<br>- Label flipping<br>- Membership inference</p> | Attacker manipulates labels to bias model behavior. Infer if specific data was used. | <p>Model misclassification<br>Privacy breach</p>     | <p>Data validation<br>Robust training<br>DP (Differential Privacy)</p> |
| **Unsupervised Learning** | <p>- Outlier injection<br>- Cluster boundary manipulation</p>         | Inject anomalous data to corrupt clustering/grouping.                                | <p>Poor clustering<br>Faulty feature engineering</p> | <p>Anomaly detection<br>Noise-tolerant algorithms</p>                  |

***

## II. 📈 Problem Type (Regression vs. Classification)

| Type               | Threat Vectors                                         | Threat Description                                                | Impact                                 | Mitigation                                                                |
| ------------------ | ------------------------------------------------------ | ----------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------------------- |
| **Regression**     | <p>- Output manipulation<br>- Adversarial outliers</p> | Inject values that skew the curve drastically.                    | Bad predictions in finance/forecasting | <p>Robust statistics<br>Outlier detection</p>                             |
| **Classification** | <p>- Evasion attacks<br>- Model inversion</p>          | Modify input to shift to a wrong class. Extract features via API. | <p>Fraud evasion<br>PII leakage</p>    | <p>Adversarial training<br>API rate limiting<br>Confidence thresholds</p> |

***

## III. 🧠 Model Concepts

| Concept                                | Threat Vectors                                                   | Threat Description                                          | Impact                                         | Mitigation                                                           |
| -------------------------------------- | ---------------------------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------- | -------------------------------------------------------------------- |
| **Overfitting**                        | <p>- Model memorizes sensitive data<br>- Poor generalization</p> | Attacker recovers training data or causes high test error   | <p>Privacy loss<br>Performance degradation</p> | <p>Regularization<br>Cross-validation</p>                            |
| **Decision Trees**                     | <p>- Path probing<br>- Rule extraction</p>                       | Reveal logic via output observation                         | <p>IP theft<br>Gaming the model</p>            | <p>Ensemble methods<br>Access control</p>                            |
| **Boosting (e.g., XGBoost, AdaBoost)** | - Cascade poisoning                                              | Poison early weak learners to propagate error               | Biased final model                             | <p>Early stopping<br>Data sanitization</p>                           |
| **Loss Functions**                     | <p>- Gradient manipulation<br>- Label flipping</p>               | Craft data to drive optimizer to suboptimal minima          | Inaccurate predictions                         | Robust loss functions (e.g., MAE over MSE)                           |
| **Gradient Descent**                   | <p>- Adversarial gradients<br>- Model extraction</p>             | Steer model via poisoned gradients                          | <p>Backdoors<br>Loss of confidentiality</p>    | <p>DP-SGD<br>Gradient clipping</p>                                   |
| **Neural Networks**                    | <p>- Adversarial examples<br>- Backdoors<br>- Trojans</p>        | Minor perturbations trick model; implant malicious behavior | <p>Model unreliability<br>Trust violation</p>  | <p>Adversarial training<br>Activation analysis<br>Neuron pruning</p> |

***

## IV. 🧪 Training & Feature Engineering

| Concept                                         | Threat Vectors                                                   | Threat Description                                           | Impact                                                 | Mitigation                                                     |
| ----------------------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ | -------------------------------------------------------------- |
| **Feature Engineering**                         | <p>- Feature poisoning<br>- Feature leakage</p>                  | Craft features to mislead the model; leak sensitive features | <p>Model skew<br>Privacy violations</p>                | <p>Feature selection audit<br>Leakage checks</p>               |
| **Dimensionality Reduction (e.g., PCA, t-SNE)** | <p>- Component injection<br>- Visualization deception</p>        | Add noisy directions to alter embedding                      | <p>False data interpretation<br>Attack obfuscation</p> | <p>Robust PCA<br>Manual component review</p>                   |
| **Training Data Pipeline**                      | <p>- Data poisoning<br>- Supply chain attacks</p>                | Replace or corrupt data at ingestion stage                   | Compromised training                                   | <p>Versioning<br>Hash validation<br>Secure pipeline</p>        |
| **Label Generation**                            | <p>- Crowdsourcing manipulation<br>- Scripted label flipping</p> | Skewed labels via malicious labelers                         | Garbage-in-garbage-out                                 | <p>Active learning<br>Quality control<br>Human-in-the-loop</p> |

***

## V. ⚙️ Attack Techniques Across Lifecycle

| Phase                 | Threat Type                               | Example                                          | Mitigation                                              |
| --------------------- | ----------------------------------------- | ------------------------------------------------ | ------------------------------------------------------- |
| **Data Collection**   | Poisoning / Privacy attacks               | Malicious contributors to training set           | <p>Provenance tracking<br>DP</p>                        |
| **Model Training**    | Gradient-based attacks                    | Introduce poisoned gradients                     | <p>DP-SGD<br>Gradient clipping</p>                      |
| **Model Inference**   | Adversarial inputs / Membership inference | Perturbed images to evade detection              | <p>Confidence thresholds<br>Noise-tolerant training</p> |
| **Model Deployment**  | Model extraction / API abuse              | Black-box API probing                            | <p>Rate limiting<br>Access controls</p>                 |
| **Model Maintenance** | Concept drift exploitation                | Gradual poisoning of continuously trained models | <p>Drift detection<br>Human audit</p>                   |

***

## VI. 📦 Advanced Considerations

| Area                                  | Threat                                    | Example                                    | Countermeasure                                         |
| ------------------------------------- | ----------------------------------------- | ------------------------------------------ | ------------------------------------------------------ |
| **Model Explainability (SHAP, LIME)** | Model stealing via explanations           | Output interpretation helps recreate model | <p>Limit granularity<br>Explainability abstraction</p> |
| **AutoML**                            | Auto-poisoning                            | Exploiting the automation loop             | <p>Human verification<br>Dataset whitelisting</p>      |
| **Transfer Learning**                 | Pretrained model backdoors                | Pretrained on poisoned corpora             | <p>Re-train last layers<br>Audit source</p>            |
| **Federated Learning**                | <p>Malicious clients<br>Model leakage</p> | Poisoned local updates                     | <p>Secure aggregation<br>Client vetting</p>            |

***

## VII. 🔍 Prioritized Risk Assessment (STRIDE-Like)

| Threat Type                | Examples in ML Context                    | Security Property Violated |
| -------------------------- | ----------------------------------------- | -------------------------- |
| **Spoofing**               | Fake clients in federated learning        | Authentication             |
| **Tampering**              | Data poisoning, gradient manipulation     | Integrity                  |
| **Repudiation**            | Malicious labeling with no accountability | Non-repudiation            |
| **Information Disclosure** | Membership inference, model inversion     | Confidentiality            |
| **Denial of Service**      | Flooding API with adversarial inputs      | Availability               |
| **Elevation of Privilege** | Exploiting AutoML or deployment pipelines | Authorization              |

***

## 🛠️ Threat Map&#x20;

<div data-full-width="true"><img src="images/Impact_Mapping.jpg" alt="Day 1-20 Recap" width="563"></div>
