# 🏢 Gemini MongoDB Chatbot with FastAPI - RAG modal

This project is a **Real Estate Expert Chatbot** built using **FastAPI**, **MongoDB**, **Gemini API (Google Generative AI)**, and **FAISS** for semantic search.  
It retrieves rules and guidelines from a knowledge base stored in MongoDB, embeds them into vectors for similarity search, and generates contextual answers with Gemini.  

The chatbot also maintains a **conversation history** (saved in `history.json`) and provides a simple **web-based UI**.

---

## 🚀 Features
- 🔹 **FastAPI Backend** with REST endpoints
- 🔹 **MongoDB Knowledge Base** for storing building rules
- 🔹 **Gemini Embeddings + FAISS** for semantic search
- 🔹 **LLM Integration** using Google Gemini (`gemini-2.5-flash-preview-05-20`)
- 🔹 **Conversation History** (persisted across restarts)
- 🔹 **Web UI** for interactive chat
- 🔹 **Toggleable Q&A History Panel** in sidebar

---

## 🛠️ Tech Stack
- **FastAPI** – Backend framework  
- **MongoDB Atlas** – Cloud database for storing chunks of legal rules document  
- **FAISS** – Vector similarity search for document retrieval  
- **Google Generative AI (Gemini)** – LLM for answering questions  
- **Pydantic** – Request validation  
- **Deque (collections)** – Conversation history buffer  
- **HTML + JavaScript** – Simple frontend  

---

## 📂 Project Structure
```
.
├── main.py           # FastAPI backend with endpoints
├── history.json      # Stores recent conversation history (auto-created)
└── README.md         # Project documentation
```

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/gemini-mongodb-chatbot.git
cd gemini-mongodb-chatbot
```

### 2️⃣ Install Dependencies
Make sure you have **Python 3.9+** installed.  
Install required packages:
```bash
pip install fastapi uvicorn pymongo faiss-cpu google-generativeai pydantic
```

### 3️⃣ Configure API Keys & Database
- Get a **Google Gemini API key** from [Google AI Studio](https://aistudio.google.com/).  
- Update the key inside `main.py`:
  ```python
  genai.configure(api_key="YOUR_GEMINI_API_KEY")
  ```
- Update the MongoDB connection string in `main.py`:
  ```python
  mongo_uri = "your_mongodb_atlas_connection_uri"
  ```

### 4️⃣ Run the FastAPI App
```bash
uvicorn main:app --reload
```

The API will start at:  
👉 `http://127.0.0.1:8000/`

### 5️⃣ Open the Web UI
Visit in your browser:  
👉 `http://127.0.0.1:8000/`

---

## 🔗 API Endpoints

### `POST /ask`
Ask a question to the chatbot.
- **Request Body**:
```json
{
  "question": "What are the building height restrictions?"
}
```
- **Response**:
```json
{
  "answer": "The maximum building height is 30 meters..."
}
```

### `GET /history`
Retrieve the recent conversation history.
- **Response**:
```json
{
  "history": [
    {"question": "Q1...", "answer": "A1..."},
    {"question": "Q2...", "answer": "A2..."}
  ]
}
```

### `GET /`
Returns the web-based chat UI.

---

## 💾 Data Ingestion
Your **MongoDB collection** (`Building_Rules`) should contain documents like:
```json
{
  "chunk_number": 1,
  "content": "Buildings should have at least 2.5m clearance..."
}
```
The startup event will automatically fetch and embed these chunks into FAISS.

---

## 🧠 Conversation History
- Maintains **last 3 question-answer pairs** (`MAX_HISTORY = 3`).
- Stored in `history.json`.
- Automatically loaded on startup.

---

## 📸 UI Preview
The chat interface contains:
- **Sidebar** → Recent Q&A history with toggle show/hide answers.  
- **Chat Panel** → Ask questions and receive bot responses.  

---

## 📝 Future Improvements
- ✅ Add user authentication  
- ✅ Store chat logs in MongoDB instead of local JSON  
- ✅ Enhance UI with React or Vue.js  
- ✅ Add support for multi-turn memory beyond 3 exchanges  

---

## Author
- Yogesh. G
