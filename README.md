# Abstractive-Text-Summarization-with-Fine-Tuned-BART

This project presents an abstractive text summarization system built using a fine-tuned BART (Bidirectional and Auto-Regressive Transformers) model. The goal is to generate concise and meaningful summaries from long textual inputs while preserving semantic content and readability.


## Project Resources

- **Dataset:** CNN/DailyMail (via HuggingFace Datasets)  
  https://huggingface.co/datasets/cnn_dailymail


## Problem Overview

With the rapid growth of textual data, extracting relevant information efficiently has become increasingly challenging. This project addresses the problem of **abstractive text summarization**, where the objective is to generate new, coherent sentences that capture the key ideas of long documents.


## Model Architecture

The project utilizes the **BART model**, introduced by Lewis et al. (2019), which combines:

- A **bidirectional encoder** (understanding context)
- An **autoregressive decoder** (generating summaries)

This architecture makes BART particularly effective for sequence-to-sequence tasks such as summarization.


## Methodology

### Data Preprocessing
- Dataset inspection and cleaning
- Statistical analysis of sequence lengths
- Tokenization using BART tokenizer
- Max input length: **512 tokens**
- Max summary length: **128 tokens**

### Data Representation
Each sample is transformed into:
- `input_ids`
- `attention_mask`
- `labels`

## Training Strategy

### Initial Attempt
- Full dataset (~287,000 samples) was used
- Batch size = 2 (to prevent GPU overflow)
- ❌ Training could not complete due to resource limitations

### Optimized Training
To address computational constraints:

- Dataset reduced to **20,000 samples**
- Batch size increased to **4**
- Gradient accumulation steps = **4**
- Effective batch size = **16**
- Learning rate = **3e-5**
- Epochs = **1**

### Key Techniques

- **Gradient Accumulation:** Simulates larger batch size under limited GPU memory
- **Mixed Precision (FP16):** Improves training speed and reduces memory usage
- **Checkpointing:** Saves progress during training to prevent data loss


## Evaluation

Model performance was evaluated using ROUGE metrics:

- **ROUGE-1:** 0.25  
- **ROUGE-2:** 0.12  
- **ROUGE-L:** 0.20

<img width="508" height="338" alt="Screenshot 2026-04-10 at 22 12 13" src="https://github.com/user-attachments/assets/82f863c9-8e68-459c-8bdb-5387c31a06e9" />


### Observations

- Model captures main ideas effectively
- Generates coherent and readable summaries
- Struggles with fine-grained details and non-news text

##  Demo Application

A simple interactive interface was built using **Gradio**.

Features:
- Input custom text
- Generate summaries in real-time
- Basic preprocessing
- Word count statistics

<img width="1254" height="791" alt="Screenshot 2026-04-10 at 22 09 54" src="https://github.com/user-attachments/assets/8501835c-6481-4954-a927-6d96aada145f" />

