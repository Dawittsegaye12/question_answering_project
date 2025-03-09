# RAG-based Question Answering with Natural Questions Dataset

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG)** model for **question answering** using the **Natural Questions** dataset. The RAG model combines a **retriever** to find relevant documents and a **generator** to generate answers based on the retrieved documents.

The retriever component utilizes **Dense Passage Retrieval (DPR)** and **FAISS** for efficient similarity search to fetch relevant documents (such as Wikipedia passages) for a given query. The generator component, which can be based on **T5** or **BART**, then generates answers from the retrieved documents.

The goal of this project is to combine these models into an end-to-end pipeline that can efficiently answer questions based on large external knowledge bases.

## Features:
- **Retriever**: Uses Dense Passage Retrieval (DPR) to retrieve relevant passages for a question.
- **Generator**: Uses T5 or BART to generate an answer based on the retrieved passages.
- **End-to-End Pipeline**: Combines retrieval and generation to form a complete RAG system.
- **Fine-Tuning**: Supports fine-tuning both the retriever and generator on the **Natural Questions** dataset.
- **Evaluation**: Includes evaluation scripts to assess the model’s performance using metrics like **F1 score**, **ROUGE**, and **BLEU**.
