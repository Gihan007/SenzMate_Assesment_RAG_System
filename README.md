--------------CHECK IMPORTENT TXT FOR USE ALL THE API KEYS THAT NEED TO RUN THIS PROJECT --------------
-------------- ALSO I PROVIDED ONE PDF AND ITS DOCX FILE TOO FOR DEMO PURPOSE -------------------------

# Document-Based Question Answering Application 📚🚀

A Streamlit web app that allows users to upload documents (PDF, DOCX, TXT, Text input, or URLs) and ask intelligent questions. It processes the input using vector embeddings stored in Weaviate and answers queries with Groq's Llama AI model.


## Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Installation](#installation)
* [Usage](#usage)
* [Methodology & Workflow](#methodology--workflow)
* [How the Interface Works](#how-the-interface-works)
* [Project Flow](#project-flow)
* [API Keys](#api-keys)
* [Tech Stack](#tech-stack)
* [Author](#author)

---

## Overview

This application enables retrieval-augmented generation (RAG) by ingesting documents or webpages, converting them into vector embeddings stored in a Weaviate database, and then answering user queries with a LLM (Large Language Model) provided by Groq.

Users can upload files or provide links, which are processed and split into text chunks, converted to embeddings, and stored for fast retrieval.

---

## Features

* Supports multiple input types: PDF, DOCX, TXT, raw Text, and URLs
* Splits documents into chunks to optimize embeddings
* Uses HuggingFace embeddings for vectorization
* Stores vectors in a managed Weaviate instance
* Answers questions using Groq's Llama-4 Maverick model
* Interactive and visually appealing Streamlit frontend with animations
* Custom CSS styling for UI/UX enhancements

---

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Gihan007/SenzMate_Assesment_RAG_System.git
cd SenzMate_Assesment_RAG_System
```

2. Create and activate a Python virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

3. Install the required packages:

```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the project root and add your API keys:

```
HUGGINGFACE_API_KEY=your_huggingface_api_key_here
GROQ_API_KEY=your_groq_api_key_here
WEAVIATE_URL=your_weaviate_instance_url
WEAVIATE_API_KEY=your_weaviate_api_key
```

---

## Usage

Run the Streamlit app:

```bash
streamlit run app.py
```

* Select your input type in the sidebar (PDF, Text, DOCX, TXT, or Link).
* Upload your file(s) or paste your URLs or text.
* Click **Proceed** to process and store the vector embeddings.
* Once the vector store is created, ask your questions in the input box.
* Click **Submit** to get AI-generated answers based on your documents.

---

## Methodology & Workflow

### 1. Environment Setup & API Keys

* Load environment variables using `dotenv` to keep API keys secure.
* Keys needed:

  * HuggingFace API for embeddings
  * Groq API for LLM responses
  * Weaviate API for vector DB connection

### 2. Input Handling & Document Loading (`process_input`)

* Based on selected input type:

  * **Link:** Load webpage content using `WebBaseLoader`.
  * **PDF:** Extract text from all pages using `PyPDF2`.
  * **Text:** Accept raw text input.
  * **DOCX:** Extract paragraphs using `python-docx`.
  * **TXT:** Read raw text from uploaded file.
* Input is converted into a list of document strings.

### 3. Text Splitting

* Use `CharacterTextSplitter` to split documents into chunks of 1000 characters with 100 characters overlap.
* This prevents memory overflow and helps embeddings capture local context.

### 4. Embeddings Generation

* Use `HuggingFaceEmbeddings` to convert text chunks into dense vector representations.
* This transforms text into a numerical format that captures semantic meaning.

### 5. Vector Store Creation (`Weaviate`)

* Connect to Weaviate instance with API key.
* Store text chunks and their embeddings in Weaviate for efficient semantic search.
* Ensure connection readiness before proceeding.

### 6. Querying & Answer Generation (`answer_question`)

* Retrieve top relevant documents for the user's query from the vector store.
* Combine these documents into a context string.
* Use Groq's Llama 4 Maverick model with prompt engineering to answer based only on provided context.
* Clean output by removing unwanted tags and formatting.

### 7. Streamlit Frontend

* Intuitive UI with sidebar for input type selection and data entry.
* Interactive buttons to proceed and ask questions.
* Display answers in styled chat bubbles.
* Lottie animations and custom CSS for polished look.

---

## How the Interface Works

The user interface is built using Streamlit, providing a simple and interactive experience:

* **Sidebar Controls:** Users select the type of input (PDF, DOCX, TXT, raw Text, or URL) from a dropdown menu in the sidebar.
* **Input Area:** Depending on selection, users upload files, enter URLs, or paste raw text.
* **Processing Button:** A **Proceed** button triggers document processing, splitting, embedding, and storage.
* **Question Input:** After processing, a text input box appears for the user to enter questions related to their uploaded documents.
* **Answer Display:** Answers from the AI model are shown as chat bubbles on the main page, along with animations to enhance engagement.
* **Custom Styling:** The UI uses custom CSS for colors, fonts, and layouts to improve readability and user experience.

---

## Project Flow

Below is a high-level flow describing how data moves through the system and how the components interact:

```
User Input (PDF/DOCX/TXT/Text/URL)
        ↓
 Document/Text Extraction & Loading
        ↓
 Text Splitting into Chunks (overlapping)
        ↓
 Embeddings Generation (HuggingFace API)
        ↓
Store Embeddings + Text Chunks → Weaviate Vector Database
        ↓
 User Asks Question → Query Sent to Weaviate
        ↓
Retrieve Top Relevant Text Chunks (Semantic Search)
        ↓
Context + Question Sent → Groq Llama-4 Maverick Model (LLM)
        ↓
 AI-Generated Answer Returned
        ↓
 Display Answer on Streamlit UI
```

### Description:

1. **User Input:** Users upload documents or enter URLs or text.
2. **Extraction:** Text is extracted and cleaned from inputs.
3. **Splitting:** Text is split into manageable chunks to preserve context.
4. **Embedding:** Each chunk is converted into a dense vector using HuggingFace embeddings.
5. **Storage:** Vectors and chunks are stored in Weaviate for efficient search.
6. **Query:** User questions trigger semantic search against stored embeddings.
7. **Answering:** Top chunks retrieved provide context to the LLM, which generates answers.
8. **Output:** Answers are shown interactively in the frontend.

---

## API Keys

* **HuggingFace:** [Get API key](https://huggingface.co/settings/tokens) for embeddings
* **Groq:** Obtain from [Groq platform](https://groq.com/)
* **Weaviate:** Managed cloud instance URL and API key (or self-hosted)

---

## Tech Stack

* Python 3.8+
* Streamlit (Frontend)
* Weaviate (Vector DB)
* Groq LLM API (AI Answers)
* LangChain community modules (document loading & splitting)
* PyPDF2, python-docx (document parsing)
* HuggingFace embeddings (text vectorization)

---

## Author

Developed by **Gihan Lakmal**
Demo for SenzMate Interview Assessment 🚀


