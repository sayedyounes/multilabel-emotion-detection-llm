## Experiment Tracking (Weights & Biases)

All experiments for this assignment were tracked using Weights & Biases (WandB).
Separate runs were created for each notebook (Parts A–C), logging inference parameters,
validation metrics (macro F1), and test set statistics.

**Public WandB Project:**  
https://wandb.ai/account-settings/younes-hoseini67-university-of-texas-at-dallas-org/members
link for one of project:
https://wandb.ai/younes-hoseini67-university-of-texas-at-dallas/emotion-detection?nw=nwuseryouneshoseini67
screenshot of main page:
 
 
 
________________________________________________________///////////||||||||||
Summary and README:
# Multilabel Emotion Classification with Gemma-2-2B and vLLM
## Overview
This project demonstrates inference and evaluation of a decoder-only large language model
for a multilabel text classification task. The goal is to predict one or more emotion labels
for each input text using a base instruction-style language model and high-performance inference.
The workflow follows the required pipeline:
dataset loading, model inference with guided decoding, validation using multilabel metrics,
and test-set prediction for Kaggle submission.

## Dataset
We use the StackExchange Emotion dataset, where each text sample may belong to multiple
emotion categories. The task is formulated as a multilabel classification problem with
the following 11 emotion classes:
- anger  
- anticipation  
- disgust  
- fear  
- joy  
- love  
- optimism  
- pessimism  
- sadness  
- surprise  
- trust  
## Model
The base **Gemma-2-2B** decoder-only language model (`google/gemma-2-2b`) is used without
fine-tuning. The model is prompted using an instruction-based format to perform emotion
classification.
Part A – Classification Head
•	Fine-tuned decoder model with classification head 
•	Binary outputs for each emotion 
•	Notebook:
PartA_Classification_Head.ipynb 
 
🔹 Part B – Language Modeling Head
•	Reformulated classification as text generation 
•	Labels generated as text (e.g., “complies” / “violates”) 
•	Used constrained decoding 
Notebooks:
•	PartB_Training_Language_Head.ipynb 
•	PartB_Inference_vLLM.ipynb 
 
🔹 Part C – Instruction-Tuned Model
•	Instruction-based prompting with decoder model 
•	Generates structured outputs (emotion labels) 
Notebooks:
•	PartC_Training_Instruction_Model.ipynb 
•	PartC_Inference_Instruction_vLLM.ipynb
## Inference with vLLM
Inference is performed using **vLLM**, enabling efficient batch generation and scalable
evaluation. Prompts are constructed in an instruction format, and predictions are generated
in batches to improve throughput.

## Guided Decoding
To ensure valid and structured outputs, **JSON-guided (constrained) decoding** is applied.
The model is instructed to return emotion labels strictly as a JSON array. This reduces
invalid outputs and simplifies downstream parsing for multilabel evaluation.

## Evaluation
Model performance is evaluated on a validation set using **macro F1 score**, which is
appropriate for multilabel classification with class imbalance. Confusion matrices are
used for qualitative analysis of per-class prediction behavior.

Validation and test results are logged using **Weights & Biases (WandB)** for experiment
tracking and reproducibility.

## Test Set and Kaggle Submission
The trained inference pipeline is applied to the test dataset, and predictions are converted
into the required Kaggle submission format with one binary column per emotion label.
The final submission is evaluated on the Kaggle leaderboard.

## Summary
This project demonstrates:
- Multilabel emotion classification using a decoder-only LLM
- High-performance inference with vLLM
- Structured output enforcement via guided decoding
- Proper multilabel evaluation using macro F1
- End-to-end test inference and Kaggle submission

