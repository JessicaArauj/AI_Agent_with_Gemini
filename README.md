# AI Agent with Gemini

This project implements an **AI Agent** using the **Gemini** model via `langchain-google-genai`. It was developed to function as a **service desk triage agent** for **Lanx Capital**, processing questions about internal policies and classifying requests according to predefined rules. Additionally, the project supports **RAG (Retrieval-Augmented Generation)**, enabling answers based on uploaded and processed PDF documents.

---

## Features
- **Message Classification (Screening)**  
  - Categorizes requests into:  
    - `HIGH_SCALABLE`: Clear and objective questions about policies.  
    - `REQUEST_INFORMATION`: Vague or incomplete requests.  
    - `OPEN_TICKET`: Requests for exceptions, approvals, or ticket creation.  
  - Assigns an **urgency level** (`LOW`, `MEDIUM`, `HIGH`).  
  - Identifies missing fields to complete the request.  
- **PDF Integration**  
  - Reads internal PDF documents.  
  - Splits documents into **chunks** for optimized search and embeddings.  
- **RAG (Retrieval-Augmented Generation)**  
  - Creates a **vector store using FAISS**.  
  - Provides contextual responses based on document content.  
  - Returns `"I don't know"` if there is insufficient context.  

---

## Installation
The project is designed to run on **Google Colab**. Install dependencies with:

````bash
!pip install -q --upgrade langchain langchain-google-genai google-generativeai
!pip install -q --upgrade langchain_community faiss-cpu langchain-text-splitters PyMuPDF
````


## Main Structure

- **Model Definition**: Configuration of `ChatGoogleGenerativeAI` (Gemini).  
- **Screening**: Prompt and function for message classification.  
- **Document Loading**: Reading and processing PDFs using `PyMuPDFLoader`.  
- **Chunking**: Splitting documents with `RecursiveCharacterTextSplitter`.  
- **Embeddings**: Generating embeddings with `GoogleGenerativeAIEmbeddings`.  
- **Vector Store**: Storing embeddings in FAISS for efficient retrieval.  
- **RAG**: Chain for retrieval and contextual response generation.


## Configuration

Set your Gemini API key before running:

```python
from google.colab import userdata
GOOGLE_API_KEY = userdata.get('GEMINI_API_KEY')
````
In Colab, you can save the key in User Data to avoid exposing it directly in the code. Additionally, make sure to upload your PDF files to the Colab environment so they can be processed by the agent. You can do this by either using the Colab file upload interface or mounting Google Drive.

## Notes

- This project is a **prototype** and should not be used in production without security adjustments.  
- A valid **Google Gemini API key** is required.  
- Responses may vary depending on the content of uploaded documents.

## License

This project is licensed under the **MIT License**. You are free to use, modify, and distribute it as needed.



