# DistilBERT Phishing Mail Detection

## Overview

This project presents a deep learning-based phishing email detection system built using **DistilBERT**, a lightweight and efficient transformer model. The model is fine-tuned to classify emails as either **Phishing** or **Legitimate**, helping mitigate cybersecurity threats through automated detection.

With the rapid rise in email-based scams, this project demonstrates the effectiveness of Natural Language Processing (NLP) and transformer-based architectures in identifying malicious communications.

---

## Features

* Fine-tuned DistilBERT model for phishing email detection.
* High-performance binary text classification using transformer-based NLP.
* End-to-end pipeline including preprocessing, training, and evaluation.
* Implemented using PyTorch and Hugging Face Transformers.
* Notebook-based workflow for reproducibility and experimentation.
* Exportable trained model for deployment and inference.
* Scalable solution adaptable to real-world applications.

---

## Project Structure

```
DistilBERT-Phishing-Mail-Detection/
│
├── phising.ipynb              # Jupyter Notebook containing model training and evaluation
├── README.md                  # Project documentation
├──requirements.txt            # List of dependencies
```

---

## Dataset

The model is trained on the Phishing Email Dataset available on Kaggle.

Dataset Link:
[https://www.kaggle.com/datasets/tommyf1/phishing-email-dataset](https://www.kaggle.com/datasets/tommyf1/phishing-email-dataset)

### Dataset Description

The dataset consists of labeled email messages categorized as phishing or legitimate.

| Feature    | Description                                           |
| ---------- | ----------------------------------------------------- |
| Email Text | Content of the email                                  |
| Label      | Indicates whether the email is phishing or legitimate |

### Preprocessing Steps

* Data cleaning and normalization
* Handling missing values
* Tokenization using DistilBERT tokenizer
* Label encoding for binary classification
* Train-validation-test split

---

## Model Architecture

* **Model:** DistilBERT (`distilbert-base-uncased`)
* **Task:** Binary Text Classification
* **Framework:** Hugging Face Transformers
* **Backend:** PyTorch

DistilBERT provides a balance between speed and performance, making it suitable for real-time phishing detection systems.

---

## Installation

### Prerequisites

Ensure Python 3.8 or higher is installed.

### Steps

```bash
# Clone the repository
git clone https://github.com/ShreyaVerm-a/DistilBERT-Phishing-Mail-Detection.git

# Navigate into the project directory
cd DistilBERT-Phishing-Mail-Detection

# Install required dependencies
pip install -r requirements.txt
```

---

## Usage

### Run the Notebook

```bash
jupyter notebook phising.ipynb
```

Execute all cells to preprocess data, train the model, and evaluate performance.

---

## Model Download

Due to GitHub's file size limitations, the trained model, tokenizer, weights, and vocabulary are hosted on Google Drive.

**Google Drive Link:**
[https://drive.google.com/drive/folders/1A1Uvz9HJsbLRELJA8TjiDy4gLlQHNe0Z?usp=sharing](https://drive.google.com/drive/folders/1A1Uvz9HJsbLRELJA8TjiDy4gLlQHNe0Z?usp=sharing)

### Expected Directory Structure

```
phishing-model/
├── config.json
├── model.safetensors
├── tokenizer.json
├── tokenizer_config.json
├── vocab.txt
└── special_tokens_map.json
```

---

## Loading the Trained Model

```python
from transformers import DistilBertTokenizerFast, DistilBertForSequenceClassification

model_path = "path_to_downloaded_model"

tokenizer = DistilBertTokenizerFast.from_pretrained(model_path)
model = DistilBertForSequenceClassification.from_pretrained(model_path)
```

---

## Example Inference

```python
import torch
from transformers import DistilBertTokenizerFast, DistilBertForSequenceClassification

model_path = "path_to_downloaded_model"

tokenizer = DistilBertTokenizerFast.from_pretrained(model_path)
model = DistilBertForSequenceClassification.from_pretrained(model_path)

email_text = "Your account has been suspended. Click the link to verify immediately."

inputs = tokenizer(email_text, return_tensors="pt", truncation=True, padding=True)
outputs = model(**inputs)

prediction = torch.argmax(outputs.logits, dim=1).item()
label = "Phishing" if prediction == 1 else "Legitimate"

print("Prediction:", label)
```

---

## Training Hyperparameters

The DistilBERT model was fine-tuned using the Hugging Face `Trainer` API with the following configuration:

| Hyperparameter           | Value                     |
| ------------------------ | ------------------------- |
| Model                    | distilbert-base-uncased   |
| Output Directory         | `./results`               |
| Number of Epochs         | 4                         |
| Training Batch Size      | 16                        |
| Evaluation Batch Size    | 16                        |
| Learning Rate            | 2e-5                      |
| Weight Decay             | 0.01                      |
| Logging Steps            | 10                        |
| Evaluation Strategy      | Enabled during training   |
| Push to Hugging Face Hub | Disabled                  |
| Reporting                | None                      |
| Framework                | PyTorch                   |
| Trainer API              | Hugging Face Transformers |


---

## Model Evaluation Results

The model was evaluated on the test dataset using standard classification metrics.

### Performance Summary

| Metric                    | Score |
| ------------------------- | ----- |
| Accuracy                  | 0.98  |
| Precision (Safe)          | 0.99  |
| Precision (Phishing)      | 0.96  |
| Recall (Safe)             | 0.97  |
| Recall (Phishing)         | 0.98  |
| F1-Score (Safe)           | 0.98  |
| F1-Score (Phishing)       | 0.97  |
| Macro Average F1-Score    | 0.98  |
| Weighted Average F1-Score | 0.98  |
| Test Samples              | 2,798 |



---

## Technologies Used

| Category                   | Tools & Libraries         |
| -------------------------- | ------------------------- |
| Programming Language       | Python                    |
| Deep Learning Framework    | PyTorch                   |
| NLP Framework              | Hugging Face Transformers |
| Data Processing            | Pandas, NumPy             |
| Machine Learning Utilities | Scikit-learn              |
| Development Environment    | Jupyter Notebook          |
| Dataset Source             | Kaggle                    |

---

## Future Improvements

* Deploy the model using Flask or FastAPI.
* Integrate the system into email clients and web applications.
* Experiment with advanced transformer models such as BERT and RoBERTa.
* Optimize performance using quantization and pruning.
* Build a real-time phishing detection API.
* Containerize the solution using Docker.

---

## Author

**Shreya Verma**

---

## Acknowledgments

* Hugging Face Transformers
* PyTorch
* Scikit-learn
* Kaggle for the dataset
* The open-source AI community

---
