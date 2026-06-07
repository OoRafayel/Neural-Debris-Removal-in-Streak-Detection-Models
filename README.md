# Neural Debris Removal in Streak Detection Models

This repository contains my solution for the Kaggle competition:

**Neural Debris Removal in Streak Detection Models**

---

## 1. Problem Overview

The goal of this competition is to remove backdoor behavior from a poisoned RetinaNet object detector without access to the original training data.

The model must:

- Forget trigger-based malicious behavior
- Preserve normal detection performance
- Work under a limited "unlearning set" setting

This is a typical **machine unlearning + backdoor removal** problem.

---

## 2. Key Idea

Our method is based on the observation that backdoor behavior activates specific feature channels in intermediate layers.

We design a multi-stage unlearning pipeline:

- Identify trigger-sensitive channels via activation analysis
- Perform structured channel pruning on high-risk features
- Apply backbone freezing to preserve general representations
- Use EWC to reduce catastrophic forgetting
- Introduce feature suppression loss to explicitly weaken trigger responses

---

## 3. Method Pipeline

Poisoned RetinaNet Model  
↓  
Activation / Poison Score Analysis  
↓  
Trigger-aware Channel Pruning  
↓  
Backbone Freezing  
↓  
Head Fine-tuning + EWC  
↓  
Feature Suppression Loss  
↓  
Final Unlearned Model  

---

## 4. Dataset

- Poisoned RetinaNet model (provided by competition)
- Unlearn set (20 trigger-annotated images)
- Test set (2000 images)

---

## 5. Key Components

### 5.1 Poison Score Analysis
We compute channel-level activation statistics to estimate trigger sensitivity.

### 5.2 Channel Pruning
High-risk channels are selectively removed to suppress backdoor activation.

### 5.3 EWC Regularization
Elastic Weight Consolidation is used to prevent catastrophic forgetting.

### 5.4 Feature Suppression Loss
A custom loss that penalizes trigger-region feature activation.

---

## 6. Result

Final Kaggle Performance:

- Rank: **47 / 230**
- Top: **20.4%**

---

## 7. Repository Structure
- notebook.ipynb
- submission.csv
- README.md

---

## 8. Citation

For educational and research purposes only.
