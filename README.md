# RAG-based Question Answering with Stanford Question Answering Dataset (SQuAD)

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG)** model for **question answering** using the **Stanford Question Answering Dataset (SQuAD)**. The RAG model combines a **retriever** to find relevant documents and a **generator** to generate answers based on the retrieved documents.

The retriever component utilizes **Dense Passage Retrieval (DPR)** and **FAISS** for efficient similarity search to fetch relevant documents (such as Wikipedia passages) for a given query. The generator component, which can be based on **T5** or **BART**, then generates answers from the retrieved documents.

The goal of this project is to combine these models into an end-to-end pipeline that can efficiently answer questions based on large external knowledge bases.

## Features:
- **Retriever**: Uses Dense Passage Retrieval (DPR) to retrieve relevant passages for a question.
- **Generator**: Uses T5 or BART to generate an answer based on the retrieved passages.
- **End-to-End Pipeline**: Combines retrieval and generation to form a complete RAG system.
- **Fine-Tuning**: Supports fine-tuning both the retriever and generator on the **Stanford Question Answering Dataset (SQuAD)**.
- **Evaluation**: Includes evaluation scripts to assess the model’s performance using metrics like **F1 score**, **ROUGE**, and **BLEU**.

---

## Preprocessing Steps

This section outlines the steps taken to preprocess the **Stanford Question Answering Dataset (SQuAD)** for use with a **Retrieval-Augmented Generation (RAG)** model, which consists of two parts: a **retriever** and a **generator**.

### 1. Load the Dataset

First, we load the **Stanford Question Answering Dataset (SQuAD)** using the [datasets library](https://huggingface.co/docs/datasets/), which makes it easy to access and handle datasets. You can also load the dataset from a CSV if it has been preprocessed and stored locally.

### 2. Text Cleaning

The questions and contexts (passages) are cleaned and tokenized. In the cleaning step, we remove any special characters, extra spaces, or unnecessary symbols from both the **questions** and **contexts**. This ensures that the text is properly formatted before feeding it into the models.

### 3. Create a Context and Query Pair

- **Retriever**: The **retriever model** (DPR) needs pairs of **contexts** (documents) and **questions** to find relevant passages for a given query. Each question is paired with its corresponding context.
- **Generator**: The **generator model** (T5 or BART) requires the combined format of **question + context** to generate an answer based on the retrieved context.

### 4. Tokenization

Tokenization is performed using pre-trained tokenizers for both the **retriever** and **generator** models:
- **DPR Retrievers**: The question and context are tokenized using the **DPRQuestionEncoderTokenizer** and **DPRContextEncoderTokenizer** to create the appropriate input embeddings.
- **T5/BART Generator**: The **T5Tokenizer** is used to tokenize the combined "question + context" input to generate answers.

### 5. Split Data into Training/Validation Sets

The data is split into **training** and **validation** sets to ensure that the models can be properly fine-tuned. The training set is used for model training, and the validation set is used to evaluate model performance during the training process.

### 6. Prepare FAISS Index for Efficient Search

The **retriever model** relies on **FAISS** (Facebook AI Similarity Search) for fast similarity searches. To efficiently retrieve relevant passages for a given query, a **FAISS index** is created from the context embeddings. The FAISS index allows the retriever to quickly search and return the top-k most relevant contexts from a large corpus.

---

This section describes the essential preprocessing pipeline for preparing the **Stanford Question Answering Dataset (SQuAD)** to work with a **Retrieval-Augmented Generation (RAG)** model. The steps outlined here help ensure that both the retriever and generator models can work effectively and efficiently on the dataset.

---

# Stanford Question Answering Dataset (SQuAD)

The **Stanford Question Answering Dataset (SQuAD)** contains a set of **reading comprehension questions** based on passages from **Wikipedia articles**. The questions are paired with a **context** (a paragraph from a Wikipedia article) and an **answer** (a text span within that context).

## Types of Questions in SQuAD Dataset:

### 1. Fact-based Questions
These questions ask for specific information directly found within the context.

**Example**:
- **Question**: "Who is the president of the United States?"
- **Answer**: "Joe Biden"

### 2. Who/What/When/Where/Why/How Questions
These are interrogative questions that ask about a specific entity, event, or circumstance.

**Example**:
- **Question**: "What year did World War II end?"
- **Answer**: "1945"

### 3. Open-ended Questions
Some questions may require more detailed responses, though the answer is still present in the text.

**Example**:
- **Question**: "How did World War II impact Europe?"
- **Answer**: "It led to widespread devastation, loss of life, and massive economic recovery efforts."

### 4. Date/Location-based Questions
Questions asking for specific times, dates, or places referenced in the context.

**Example**:
- **Question**: "When did Albert Einstein publish the theory of relativity?"
- **Answer**: "1905"

### 5. Entity Identification
These questions focus on identifying specific entities like people, places, organizations, etc.

**Example**:
- **Question**: "Which country is the Eiffel Tower located in?"
- **Answer**: "France"

### 6. Conceptual Questions
These questions may ask for understanding relationships or general concepts presented in the text.

**Example**:
- **Question**: "What is the capital of France?"
- **Answer**: "Paris"

---

The dataset contains a diverse set of factual, conceptual, and detailed questions about various topics. The goal is to answer these questions by extracting a text span from the context that directly answers the question.
