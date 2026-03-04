# Evaluating Generative Vision-Language Models for Radiology Visual Question Answering

This repository contains a comprehensive benchmarking study for **Medical Visual Question Answering (Med-VQA)** on the **VQA-RAD** dataset.

The project investigates the transition from traditional discriminative (classification-based) architectures to modern generative Vision-Language Models (VLMs), comparing performance across closed-ended safety tasks and open-ended clinical reasoning.

## 📊 Comparative Performance Results

The following table benchmarks our baseline against the proposed generative architectures:

| Model                         | Overall Accuracy | Closed-Ended (Y/N) | Open-Ended (Descriptive) |  ROUGE-L   |
| :---------------------------- | :--------------: | :----------------: | :----------------------: | :--------: |
| **CNN-LSTM + Attention**      |      34.22%      |       52.78%       |          1.23%           |   0.3467   |
| **BLIP**                      |      45.33%      |       59.72%       |          19.75%          |   0.4914   |
| **Qwen3-VL-2B-Instruct**      |    **54.67%**    |     **68.75%**     |        **29.63%**        | **0.5828** |

### Key Project Insights

- **The Vocabulary Bottleneck:** Traditional models (CNN-LSTM) suffer a "catastrophic failure" in open-ended tasks (1.23% accuracy) due to fixed-vocabulary constraints.
- **Clinical Safety:** Confusion matrix analysis shows that generative models like Qwen3-VL are more sensitive to positive findings, significantly reducing dangerous **False Negatives** compared to the baseline.
- **Data Efficiency:** Using **LoRA (Low-Rank Adaptation)** allowed the generative models to adapt to specific radiology terminology with only 5 epochs of training.

---

## 🏗️ Model Architectures

### 1. Hybrid CNN-LSTM with Attention (Baseline)

A discriminative model that treats VQA as a classification task.

- **Vision:** VGG-19 backbone.
- **Language:** LSTM network.
- **Fusion:** Tanh-based additive attention.

### 2. BLIP (Proposed Generative)

A parameter-efficient VLM fine-tuned on medical data.

- **Backbone:** OPT-2.7b LLM with a Querying Transformer (Q-Former).
- **Optimization:** LoRA (Rank 16, Alpha 32).

### 3. Qwen3-VL-2B-Instruct (SOTA Benchmark)

A state-of-the-art instruction-tuned VLM evaluated for zero-shot and few-shot capabilities in medical imaging. It demonstrated the strongest performance in descriptive "Open-Ended" clinical questions.

---

<!-- ## 📈 Visual Analysis

### Qwen3-VL Training Dynamics
The training loss for the Qwen3-VL model shows rapid and stable convergence within the first epoch, demonstrating high transfer-learning efficiency.

![Qwen3 Loss Curve](https://github.com/your-username/RadVQA-Benchmark/blob/main/path_to_loss_image.png)

### Confusion Matrix (Yes/No Questions)
Generative models exhibit a more balanced decision boundary, identifying significantly more positive instances than the baseline model.

![Confusion Matrix](https://github.com/your-username/RadVQA-Benchmark/blob/main/path_to_confusion_matrix.png) -->

---
