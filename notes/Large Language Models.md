# Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG)

## Course Overview

The LLM Zoomcamp course focuses on practical applications of Large Language Models (LLMs) and Retrieval-Augmented Generation (RAG). The primary project is to build a Q&A system that leverages FAQs from multiple courses to answer student queries efficiently. The system will use LLMs and RAG to process questions and provide accurate answers based on a knowledge base of FAQ documents.

### Problem Statement

- **Context**: The course community maintains extensive FAQ documents (e.g., 321 pages for the Data Engineering Zoomcamp) with a question-answer format organized by sections.
- **Challenge**: Finding specific answers in these large documents is inefficient, as students must manually search through numerous questions.
- **Solution**: Develop a Q&A system where users input a question via a simple form, and the system retrieves relevant FAQ content to generate accurate answers using LLMs and RAG.

### Course Goals

- Learn to use LLMs and RAG to build a Q&A system.
- Understand how to integrate a knowledge base with an LLM for context-aware responses.
- Implement the system with a user-friendly interface (e.g., Streamlit) by the course's end.
- Apply the learned concepts to a custom knowledge base.

## Understanding LLMs

### Definition

Large Language Models (LLMs) are advanced machine learning models designed to predict the next word or token in a sequence based on prior text. They are distinguished by their massive scale and ability to generate human-like responses.

### Key Characteristics

- **Scale**: LLMs have billions of parameters and are trained on vast datasets, enabling sophisticated language understanding and generation.
- **Functionality**: They predict the next word based on preceding text, making them capable of completing sentences or answering questions coherently.
- **Black Box Approach**: In this course, LLMs are treated as black boxes, focusing on their input-output behavior rather than internal mechanisms (e.g., Transformer architectures).
- **Comparison to Simple Language Models**:
  - Simple language models (e.g., those in phone keyboards) predict the next word with limited parameters and simpler algorithms (e.g., n-gram models).
  - LLMs, due to their scale, provide more accurate and contextually relevant predictions, resembling human-like understanding.

### How LLMs Work

- **Input (Prompt)**: LLMs receive text input, called a prompt, which defines the task or question.
- **Output**: The model generates a response by predicting the next logical sequence of words.
- **Prompt Structure Example**:

  ```text
  Question: How do I enroll in the course?
  Context: [Relevant FAQ content]
  Answer:
  ```

  - The LLM completes the prompt by generating an answer based on the question and provided context.
  - Modern LLMs (e.g., ChatGPT) may not require explicit "Answer:" markers, but this structure clarifies expectations for the course project.
- **Example**: Typing "How are" on a phone might suggest "you" or "there" based on common phrases. LLMs extend this concept with greater accuracy due to their extensive training.

### Applications and Limitations

- **Strengths**: LLMs excel at general knowledge tasks (e.g., "How do I cook salmon?") where they can provide comprehensive answers without external context.
- **Limitations**: LLMs struggle with specific or niche queries (e.g., "Is it too late to join the course?") without additional context, as they lack access to course-specific information.

## Exploring RAG

### Definition

Retrieval-Augmented Generation (RAG) combines **retrieval** (searching a knowledge base) with **generation** (using an LLM) to produce contextually relevant answers. The retrieval component augments the LLM’s generation by providing external information.

### Why RAG is Needed

- **LLM Limitations**: LLMs may provide vague or incorrect answers for queries requiring specific or up-to-date information (e.g., course enrollment details).
- **Role of Retrieval**: Retrieval fetches relevant documents from a knowledge base to provide the LLM with the necessary context for accurate responses.
- **Example**:
  - Query: "How do I cook salmon?"
    - LLM can answer directly using its training data.
  - Query: "How do I enroll in the Data Engineering Zoomcamp?"
    - LLM needs context from FAQ documents to provide a precise answer.

### RAG Framework

The RAG framework integrates two core components:

1. **Knowledge Base**: A repository of documents (e.g., course FAQs) containing questions and answers.
2. **LLM**: A model that generates responses based on the query and retrieved context.

### RAG Workflow

1. **User Query**:
   - A user submits a question (e.g., "How do I enroll in the course?").
2. **Retrieval**:
   - The query is sent to the knowledge base.
   - Relevant documents (e.g., D1, D2, ..., D5) are retrieved, containing FAQ entries related to the query.
3. **Prompt Construction**:
   - A prompt is created combining the query and retrieved documents:

     ```text
     Question: How do I enroll in the course?
     Context: [D1, D2, ..., D5]
     Answer:
     ```

4. **Generation**:
   - The LLM processes the prompt, using the context to generate an accurate answer.
5. **Response Delivery**:
   - The generated answer is returned to the user.

### Example Use Case

- **Scenario**: A student asks, "Is it too late to join the course?"
- **Problem**: The LLM lacks course-specific details and cannot answer accurately without context.
- **RAG Solution**:
  - Retrieve FAQ entries about enrollment deadlines.
  - Combine the query with retrieved documents in a prompt.
  - The LLM generates a precise answer based on the context.

### Flexibility of RAG

- **Knowledge Base**:
  - Initial implementation uses a simple toy search engine to demonstrate concepts.
  - Later modules upgrade to Elasticsearch for text-based search.
  - Advanced modules explore Vector search for semantic retrieval (to be covered later).
- **LLM**:
  - The course may use various LLMs, with prompts adjusted for compatibility.
  - Open-source LLMs can replace proprietary ones, requiring prompt tweaks.
- **Modularity**: The RAG framework allows swapping components (e.g., search engine or LLM) to optimize performance.

## Course Implementation Details

- **Project Objective**: Build a Q&A system for course FAQs using RAG.
- **Components**:
  - **Knowledge Base**: FAQ documents from multiple courses (e.g., Data Engineering Zoomcamp).
  - **Search Engine**:
    - Start with a toy search engine for simplicity.
    - Upgrade to Elasticsearch in later modules.
    - Explore Vector search for advanced retrieval.
  - **LLM**: Use an LLM to generate answers, with flexibility to switch models.
  - **User Interface**: Implement a simple form (e.g., using Streamlit) for question input and answer display.
- **Learning Outcomes**:
  - Understand LLM and RAG integration.
  - Build and test a Q&A system.
  - Apply the system to a custom knowledge base by the course's end.

## Additional Notes

- **Future Topics**:
  - Environment setup for running LLMs and RAG (covered in subsequent lessons).
  - Advanced retrieval techniques like Vector search for semantic understanding.
  - Customizing prompts for different LLMs.
  - Deploying the Q&A system with a user interface.
- **Practical Considerations**:
  - The course treats LLMs as black boxes, focusing on practical application over theoretical details.
  - The FAQ-based Q&A system addresses real-world inefficiencies in accessing course information.
- **Extensibility**: The RAG framework’s modularity allows experimentation with different search engines and LLMs, preparing students for real-world adaptations.

# Environment Setup for LLM and RAG

## Overview

This guide details the setup process for developing a Retrieval-Augmented Generation (RAG) system with Large Language Models (LLMs) to build a Q&A system for course FAQs. The primary setup uses GitHub Codespaces, with alternative methods using direct Python library installation locally or Miniconda/Anaconda. The Groq API is used instead of OpenAI for LLM interactions, and the provided code is tailored to Groq.

## Prerequisites

- **Python Version**: 3.12.1 (compatible with Miniconda installation).
- **Docker**: Required for later modules; pre-installed in Codespaces but needs independent installation locally.
- **GitHub Account**: Necessary for Codespaces and repository management.
- **Visual Studio Code**: Recommended for Codespaces integration or local development.
- **Groq API Key**: Required for accessing Groq's LLM services.

## GitHub Codespaces Setup

GitHub Codespaces provides a cloud-based environment with Python and Docker pre-installed, serving as the primary setup method for this course. It’s free and simplifies environment configuration.

### Steps

1. **Create a Repository**:
   - Create a public GitHub repository (e.g., `llm-zoomcamp`).
   - Set `.gitignore` to Python to exclude unnecessary files.

2. **Launch Codespaces**:
   - In the repository, navigate to "Code" > "Codespaces" > "Create Codespace on main".
   - Open in Visual Studio Code (desktop preferred; browser as fallback).
   - Install the Codespaces extension in VS Code if prompted (search for "Codespaces" in Extensions).

3. **Verify Environment**:
   - Open the terminal in VS Code (`Ctrl + ~`).
   - Confirm Docker availability:

     ```bash
     docker run hello-world
     ```

   - Check Python version:

     ```bash
     python --version  # Should return 3.12.1 or compatible
     ```

4. **Install Required Libraries**:
   - Install necessary packages via `pip`:

     ```bash
     pip install notebook==7.1.2 elasticsearch tqdm groq pandas scikit-learn
     ```

   - **Library Details**:
     - `notebook==7.1.2`: Runs Jupyter notebooks.
     - `elasticsearch`: Supports advanced search (used later).
     - `tqdm`: Provides progress bars (used in later modules).
     - `groq`: Enables Groq API interactions.
     - `pandas` and `scikit-learn`: Optional for future use.

5. **Set Up Groq API Key**:
   - Obtain an API key from [GroqCloud](https://console.groq.com/keys).
   - Set as an environment variable:

     ```bash
     export GROQ_API_KEY="your_api_key_here"
     ```

   - **Security Note**: Never commit or share the API key publicly.

6. **Start Jupyter Notebook**:
   - Launch Jupyter:

     ```bash
     jupyter notebook
     ```

   - Codespaces automatically forwards port 8888. Access via `localhost:8888` in your browser using the provided token.
   - Open or create `test.ipynb` in the `01-intro` folder.

7. **Test Groq Integration**:
   - In `test.ipynb`, run the provided code to verify Groq API connectivity:

     ```python
     from groq import Groq
     import os
     
     client = Groq()
     completion = client.chat.completions.create(
         model="meta-llama/llama-4-scout-17b-16e-instruct",
         messages=[
             {
                 "role": "user",
                 "content": "is it too late to start the course"
             }
         ],
         temperature=1,
         max_completion_tokens=1024,
         top_p=1,
         stream=True,
         stop=None,
     )
     
     for chunk in completion:
         print(chunk.choices[0].delta.content or "", end="")
     ```

   - **Notes**:
     - The code assumes `GROQ_API_KEY` is set in the environment.
     - It uses the `meta-llama/llama-4-scout-17b-16e-instruct` model with streaming for real-time output.
     - Parameters (`temperature`, `max_completion_tokens`, `top_p`) control response creativity and length (see GroqCloud [Playground](https://console.groq.com/playground)).

8. **Manage Notebooks**:
   - Save `test.ipynb` in `01-intro`.
   - Commit changes:

     ```bash
     git add 01-intro/test.ipynb
     git commit -m "Add initial notebook"
     git push
     ```

9. **Stop/Delete Codespace**:
   - Stop or delete the Codespace from GitHub’s Codespaces dashboard to save resources.

### When to Use

- Use Codespaces for:
  - A quick, cloud-based setup without local installation.
  - Pre-installed Docker and Python.
  - Seamless integration with GitHub for version control.

## Alternative Setup Options

If Codespaces is not preferred, configure the environment locally using one of the following methods.

### Option 1: Direct Python Library Installation (Local)

This method uses the system’s Python environment and `pip` for library installation, ideal for minimal local setups.

#### Steps

1. **Verify Python and Pip**:
   - Check Python version:

     ```bash
     python --version  # Should be 3.12.1
     ```

   - Verify pip:

     ```bash
     which pip
     ```

2. **Install Required Libraries**:
   - Install packages:

     ```bash
     pip install notebook==7.1.2 elasticsearch tqdm groq pandas scikit-learn
     ```

   - **Library Details**: Same as Codespaces setup.

3. **Set Up Groq API Key**:
   - Set the environment variable:

     ```bash
     export GROQ_API_KEY="your_api_key_here"
     ```

4. **Start Jupyter Notebook**:
   - Launch:

     ```bash
     jupyter notebook
     ```

   - Access via `localhost:8888` with the token.
   - Use `test.ipynb` in `01-intro`.

5. **Test Groq Integration**:
   - Run the same Groq code as in Codespaces.

#### When to Use

- Choose this option if:
  - You prefer working locally with minimal dependencies.
  - You have Python 3.12.1 installed and want control over packages.
  - Codespaces is unavailable or unsuitable.

### Option 2: Miniconda/Anaconda Installation (Local)

This method uses Miniconda (preferred) or Anaconda for a self-contained Python environment with pre-installed data science libraries.

#### Miniconda Installation (Preferred)

1. **Download Miniconda**:
   - Use the Python 3.12.1 installer:

     ```bash
     wget https://repo.anaconda.com/miniconda/Miniconda3-py312_25.3.1-1-Linux-x86_64.sh
     ```

2. **Install Miniconda**:
   - Run:

     ```bash
     bash Miniconda3-py312_25.3.1-1-Linux-x86_64.sh
     ```

   - Accept the license, follow prompts, and initialize Miniconda.
   - Verify:

     ```bash
     which python  # Should point to ~/miniconda3/bin/python
     python --version  # Should return 3.12.1
     ```

3. **Install Libraries**:
   - Miniconda includes `jupyter`, `pandas`, and `scikit-learn`. Install additional packages:

     ```bash
     pip install elasticsearch tqdm groq
     ```

4. **Set Up Groq API Key**:
   - Set:

     ```bash
     export GROQ_API_KEY="your_api_key_here"
     ```

5. **Start Jupyter Notebook**:
   - Launch: `jupyter notebook`.
   - Access via `localhost:8888` and use `test.ipynb` in `01-intro`.

6. **Test Groq Integration**:
   - Use the same Groq code.

#### Anaconda Installation (Alternative)

- **Download**: Obtain the Anaconda [installer](https://www.anaconda.com/docs/getting-started/anaconda/install#linux-installer).
- **Install**:

  ```bash
  wget <anaconda-installer-url>
  bash Anaconda3-latest-Linux-x86_64.sh
  ```

- **Note**: Anaconda is larger (~1GB) and includes unnecessary packages.
- **Install Libraries**: Same as Miniconda (`elasticsearch`, `tqdm`, `groq`).
- **API Key and Jupyter**: Follow Miniconda steps.

#### When to Use

- Use Miniconda if:
  - You want a lightweight, portable local environment.
  - You prefer minimal disk usage.
- Use Anaconda if:
  - You need a comprehensive environment with pre-installed data science tools.
  - Disk space and installation time are not concerns.

## Additional Notes

- **GPU Requirement**: Not needed for the first module but required for the second. Use GPU-enabled platforms (e.g., Google Colab, SageMaker) later.
- **Alternative Platforms**: Google Colab, SageMaker, or other notebook providers are viable alternatives to Codespaces or local setups.
- **File Organization**:
  - Store notebooks in `01-intro` (e.g., `test.ipynb`).
  - Use descriptive names for homework (e.g., `homework.ipynb`).
- **Future Topics**:
  - Indexing documents with a search engine (next unit).
  - Replacing the toy search engine with Elasticsearch.
  - Exploring Vector search and open-source LLMs.
- **Security**: Protect API keys with environment variables and avoid committing them to Git.
- **Groq API**:
  - The provided code uses streaming (`stream=True`) for real-time responses, ideal for interactive applications.
  - Parameters like `temperature=1` and `top_p=1` ensure creative but focused outputs; adjust per your preference.
  - The model `meta-llama/llama-4-scout-17b-16e-instruct` may need verification against Groq’s available models.
