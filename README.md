#  Domain-Specific RAG Chatbot for Website Knowledge

Alhamdulillah, I have successfully built an AI-powered chatbot system that intelligently answers user queries using the actual content of a specific website — in this case, [DigitalUsman.pk](https://digitalusman.pk/).

The chatbot does **not rely on pre-trained knowledge**. Instead, it crawls and scrapes the website, processes the data into vector embeddings, and uses a high-speed LLM (LLaMA 3 via Groq) to answer questions **based only on that website’s content**. This ensures that responses are accurate, up-to-date, and domain-specific.

##  Features

- Crawls and indexes every page of a given website
- Answers user questions based only on the content of the target website
- No hallucinations — answers come strictly from real data
- Uses FAISS for fast local vector similarity search
- Powered by Groq's ultra-fast LLaMA 3 70B model
- Flask backend with REST API (`/ask`)
- Chat interface built with Streamlit
- Works offline after first run (except LLM inference)

##  System Architecture & Workflow

### 1. Web Scraping  
The bot scrapes and parses all internal links using `requests` and `BeautifulSoup`, extracting text from pages like FAQs, blogs, and services.

### 2. Text Processing  
Text is split into chunks using `RecursiveCharacterTextSplitter`, optimized for embedding and retrieval.

### 3. Embedding  
Text chunks are converted into vector embeddings using HuggingFace’s `all-MiniLM-L6-v2` model.

### 4. Vector Indexing  
FAISS is used to store and retrieve document chunks based on similarity to user queries.

### 5. Language Model  
User questions + retrieved chunks are passed to **Meta’s LLaMA 3 (70B)** model using **Groq API**, which generates the final answer.

### 6. Backend  
A lightweight Flask app exposes the `/ask` POST endpoint that receives the question and returns the AI response.

### 7. Frontend  
Streamlit provides a chat UI where users can type questions and view AI responses.


##  Technologies Used

- Python  
- BeautifulSoup, Requests  
- LangChain  
- HuggingFace Transformers  
- FAISS  
- Groq API (LLaMA 3 - 70B)  
- Flask (Backend)  
- Streamlit (Frontend)  
- `.env` file for secure API key management  

---

##  Folder Structure

project-root/

├── backend/

│ ├── backend.py # Flask app

│ ├── Ai_logic.py # Web scraper + vector embeddings + QA logic

│ └── .env # API keys (GROQ_API_KEY)

│
├── frontend/

│ └── frontend.py # Streamlit chatbot UI


├── requirements.txt

└── README.md


##  Installation

```bash
git clone https://github.com/yourusername/website-ai-chatbot.git
```
cd website-ai-chatbot

## Create virtual environment (optional)
python -m venv venv
source venv/bin/activate  # On Windows use venv\Scripts\activate

## Install dependencies
pip install -r requirements.txt

 ## Setup .env
Inside the backend/ folder, create a .env file:

GROQ_API_KEY=your_groq_api_key_here
##  Run the Chatbot
Step 1: Start the backend (Flask)
cd backend
python backend.py
Step 2: Run the frontend (Streamlit)
cd frontend
streamlit run frontend.py
Go to http://localhost:8501 to chat with your AI bot.

##  Example Usage
User: "What services does DigitalUsman.pk offer?"
Bot: "DigitalUsman.pk provides web design, SEO optimization, and digital marketing services."

## Future Enhancements
Cache FAISS vectorstore to avoid scraping on every run
Add authentication and session tracking
Multi-language support

Show source URLs for context transparency
Store chat history in a database

## requirements.txt
beautifulsoup4
requests
langchain
langchain-community
langchain-groq
sentence-transformers
faiss-cpu
python-dotenv
flask
flask-cors
streamlit

##  Summary
This project demonstrates how LLMs + vector embeddings + real-time scraping can create powerful, accurate, domain-specific chatbots for any business or website.

“If you want to implement something like this for your own company, let’s collaborate.”
