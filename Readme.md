# ChatRec_Model - Conversational Response Prediction System

---

## 🚀 Project Overview

This project implements an **offline GPT-2 Transformer model** to predict User A's next reply based on the given conversational context.

---

## 📁 Directory Structure

The project repository follows this structure:

* `ChatRec_Model/`
    * `ChatRec_Model.ipynb` 📝: Jupyter notebook containing code execution.
    * `Report.pdf` 📄: Technical report summarizing model design and evaluation.
    * `Model.joblib` 💾: Serialized fine-tuned GPT-2 model and tokenizer.
    * `ReadMe.txt` (this file) 📖: Project documentation.

### Model File Link

The `Model.joblib` file is publicly available for testing and checking via this Google Drive link:
[model.joblib Google Drive Link](https://drive.google.com/file/d/11m63JoK7lzDJn_1rand-HbQrxlPMSfUj/view?usp=drive_link)

---

## ⚙️ Steps to Run

Follow these steps to run and test the conversational prediction system:

1.  **Install Dependencies** ⬇️:
    Install the necessary libraries using the command below:
    ```bash
    pip install torch transformers datasets nltk rouge-score sacrebleu pandas scikit-learn joblib tqdm
    ```
2.  **Prepare Data** 📊:
    Place your conversation dataset (e.g., `conversationfile.xlsx` or `.csv`) in the working directory.
3.  **Execute Code** ▶️:
    Run the main notebook, `ChatRec_Model.ipynb`, to preprocess data, train, and evaluate the model.
4.  **Check Output** ✅:
    After training is complete, the final model will be saved in two locations:
    * Hugging Face format: `./final_model/`
    * Serialized format: `ChatRec_Model/Model.joblib`

---

## 📊 Evaluation Summary

The model's performance on the test set is summarized by these metrics:

* **BLEU Score**: 0.0102
* **ROUGE-1**: 0.1500
* **ROUGE-2**: 0.0000
* **ROUGE-L**: 0.1000
* **Perplexity**: 53.9670

---

## 🧠 Model Justification

Key decisions regarding the model choice and deployment:

* **Model**: **GPT-2** (autoregressive Transformer).
* **Reason**: It is efficient for training on smaller datasets and capable of context-aware text generation.
* **Deployment**: **Joblib serialization** allows the model to be loaded quickly in production environments (like Flask/FastAPI).

---

## 1️⃣ Optimization

- **Model Size:** Use pre-trained GPT-2 Base or few-shot prompting; fine-tuning <20 examples is ineffective.  
- **Training Strategy:**  
  - Few-shot prompting or synthetic data augmentation.  
  - Light fine-tuning only if dataset >100 examples.  
- **Hyperparameters:** Small batch (4–8), low learning rate (~1e-5), 2–5 epochs, early stopping.  
- **Inference Optimization:** Limit context length, use FP16 on GPU, cache repeated responses.

---

## 2️⃣ Deployment Feasibiliy

- **Model Type:** Joblib-serialized GPT-2; requires PyTorch + Transformers.  
- **Platforms:**  
  - **Flask/FastAPI**: Easy API, needs ~500MB RAM.  
  - **Serverless functions:** Base GPT-2 too heavy.  
  - **Hugging Face Inference API:** Easy scalable deployment.  
- **Latency:** CPU ~3–6s, GPU ~0.2–0.5s per response.  
- **Scaling:** Small user base → single GPU instance; large → autoscaling GPU.

---

**Note:** With <20 conversations, model performance is limited. For production, increase dataset size or use few-shot prompting.
