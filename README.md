# BERT_Finetuning_QA

This repository contains the implementation of a BERT model fine-tuned on the CoQA dataset from StanfordNLP. CoQA (Conversational Question Answering) is a challenging dataset that requires a deep understanding of context in a conversational format.

Finetuned model can be found at https://huggingface.co/basilePlus/bert-finetuned-squad

## Project Overview

This project aims to enhance BERT's capabilities in understanding and generating responses in conversational question answering scenarios when feeding a context to the model. By fine-tuning the BERT model specifically on the CoQA dataset, the model is expected to perform better in finding the answer to the question in the context compared to the standard pre-trained version.

## Setup and Installation

Note : If you are planning to run training on TPU, you will need modify some lines as specified in the script.

## Dataset

CoQA is a large-scale dataset for building Conversational Question Answering systems.

Our dataset contains 127k questions with answers, obtained from 8k conversations about text passages from seven diverse domains. The questions are conversational, and the answers are free-form text with their corresponding evidence highlighted in the passage.

Here is an overview of the dataset :

| Feature    | Details |
|------------|---------|
| **Source** | From where does the context come from (wikipedia, cnn etc.) |
| **Story** | Context in which answers can be found. Answer is always available in the context |
| **Questions** | Questions that are contextually based on the given passages. |
| **Answers** | Answers to the questions |

### Example Entry (Wikipedia - Vatican Apostolic Library)

- **Context**: "The Vatican Apostolic Library, more commonly called the Vatican Library or simply the Vat, is the library of the Holy See, located in Vatican City..."
- **Questions**: "When was the Vat formally opened?", "What is the library for?", etc.
- **Answers**: "It was formally established in 1475", "research", etc.

### Example Entry (CNN - Michael Jackson Memorabilia Auction)

- **Context**: "More than 80 Michael Jackson collectibles -- including the late pop star's famous rhinestone-studded glove from a 1983 performance -- were auctioned off..."
- **Questions**: "Where was the Auction held?", "How much did they make?", etc.
- **Answers**: "Hard Rock Cafe", "$2 million.", etc.

## Model Training
  
The script utilizes Hugging Face's transformers and accelerate libraries to fine-tune BERT on the CoQA dataset. To fine-tune the model from scratch, uncomment the relevant lines in the code, as the current setup loads the model directly from the Hugging Face Hub for quick execution.

## Performances

| Metric       | Before Fine-tuning | After Fine-tuning |
|--------------|--------------------|-------------------|
| Exact Match to attended answer  | 0%                 | 11%               |

The exact match score improvement from 0% to 11% after fine-tuning shows progress, though challenges remain due to the metric choice, which is designed for the SQuAD dataset and may not be ideally suited for CoQA:
```
metric = evaluate.load("squad")
```

