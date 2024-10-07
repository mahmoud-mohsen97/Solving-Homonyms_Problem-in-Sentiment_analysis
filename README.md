# Solving the Homonyms Problem in the Sentiment analysis task

# Introduction
The task involves solving the issue of homonyms and context ambiguity in sentiment analysis. In sentences like:
```
"I hate the selfishness in you" (Negative)
"I hate anyone who can hurt you" (Positive)
```
traditional sentiment models may misclassify due to homonyms (e.g., "hate") and lack of contextual understanding. The goal is to build a sentiment analysis model that can correctly classify such sentences by fine-tuning a pre-trained `Roberta` model on a custom dataset that includes contextual challenges, like **homonyms**.


# Data Description
The dataset used for fine-tuning was generated by `GPT-4o` specifically to include sentences that reflect challenges such as **homonyms**, **sarcasm**, and **context ambiguity**. This generated dataset was balanced, diverse, and prepared for training and validation.

  - Number of training samples: 1826
  - Number of validation samples: 457
  - Features: Text sentences and sentiment labels (positive, negative, neutral).


# Baseline Experiments
**Goal**: Evaluate the performance of an off-the-shelf pre-trained `Roberta` model on the homonyms problem.

**Approach**: The `cardiffnlp/twitter-roberta-base-sentiment-latest` model was used to classify two challenging sentences. The model correctly classified one sentence but **failed** to capture the positive sentiment in the second example due to the presence of the word `"hate"` highlighting its limitations in contextual understanding.

**Conclusion**: The baseline model performed well on straightforward sentences but struggled with homonyms and context-dependent sentences, motivating the need for fine-tuning on a more diverse dataset.


# Main Experiment
**Experiment**: Fine-Tuning `Roberta` for Sentiment Analysis.

**Goal**: Improve the model’s ability to handle homonyms and contextual nuances through fine-tuning on a custom dataset.

**Approach**:
  1. Data Preparation: The dataset was split into training (80%) and validation (20%) sets to ensure reproducibility.
  2. Model Fine-tuning: The pre-trained Roberta model was fine-tuned on this dataset for **15** epochs with a learning rate of **1e-5**. The dataset was tokenized using the `Roberta tokenizer`, and training was monitored using metrics like accuracy, F1-score, precision, and recall.
  3. Evaluation: The fine-tuned model was tested on sentences with homonyms, including the initial challenge examples.

**Results**: The fine-tuned model reached an **87%** F1-score on the validation data and correctly classified both example sentences:
```
  - Negative Sentence: "I hate the selfishness in you" — Correctly predicted as Negative.
  - Positive Sentence: "I hate anyone who can hurt you" — Correctly predicted as Positive.
```
**Conclusion**: Fine-tuning improved the model’s understanding of context and homonyms, allowing it to handle challenging sentences more effectively than the baseline model.


# Overall Conclusion
Fine-tuning `Roberta` on a dataset specifically designed to include homonyms and contextual ambiguity significantly improved the model’s performance on sentiment analysis tasks. The model correctly handled the nuances of words like `"hate"` in different contexts, resulting in more accurate sentiment predictions compared to the baseline model.


# Tools and Resources
Tools Used:
  - `transformers` library for `
twitter-roberta-base-sentiment-latest` fine-tuning from [Hugging Face](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment-latest).
  - `pandas` and `matplotlib` for dataset preprocessing and visualization.
  - `sklearn` for dataset splitting and evaluation.
  - Custom dataset generated with GPT-4o to reflect real-world challenges in sentiment analysis.


# Project Reflections
**Biggest Challenge**: Generating a dataset with sufficient diversity in homonyms and contextual challenges to ensure the model learns to differentiate between similar words in different contexts.

**Key Learning**: Fine-tuning pre-trained models on custom datasets allows them to adapt to specific challenges, such as homonyms and context-dependent sentiment, leading to better overall performance in NLP tasks.
