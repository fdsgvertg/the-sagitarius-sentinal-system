# Computer chat bot

 local-first AI companion system that runs across a **PC server** and an **Android app**, designed to provide intelligent, context-aware assistance using on-device and hybrid retrieval (RAG).

---

## 🚀 Features

* 🧠 **On-device AI (Edge RAG)** for fast responses
* 💻 **PC-based AI server** for heavy processing
* 🔍 **Semantic search** using embeddings (MiniLM ONNX)
* 📱 **Android integration** with voice + triggers
* 🌐 **Hybrid routing** (local + PC + web)
* 🔒 **Secure communication (HTTPS)** between phone and PC
* 📡 **Auto-discovery of PC server (mDNS / NSD)**

---

## 🏗️ Architecture

```
[ Android App ]
     │
     │  (HTTPS + mDNS discovery)
     ▼
[ PC Server (FastAPI + Uvicorn) ]
     │
     ├── Local AI models
     ├── Memory / embeddings
     └── External APIs (optional)
```

---

## 📁 Project Structure

```
aria/
│
├── pc_server/              # Python FastAPI backend
│   ├── main.py
│   ├── config.py
│   ├── certs/
│   └── ...
│
├── android/               # Android app (Kotlin)
│   ├── app/
│   │   ├── java/com/aria/
│   │   │   ├── rag/
│   │   │   ├── memory/
│   │   │   ├── ai/
│   │   │   └── triggers/
│   │   └── res/
│   └── ...
│
└── README.md
```

---

## ⚙️ PC Server Setup

### 1. Create virtual environment

```bash
python -m venv venv
venv\Scripts\activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run server

```bash
python -m pc_server.main
```

Server runs on:

```
https://0.0.0.0:8472
```

---

## 🔐 SSL Certificates

Make sure these exist:

```
pc_server/certs/
├── aria_server.crt
├── aria_server.key
```

If missing, generate them using your setup script.

---

## 📱 Android Setup

### Requirements

* Android Studio (latest)
* Gradle 8.4+
* AGP 8.2.2

---

### Steps

1. Open `android/` in Android Studio
2. Sync Gradle
3. Build project
4. Run on device

---

## 📡 PC Discovery (Important)

The app uses:

* **NSD / mDNS** to auto-detect PC server
* Falls back to saved IP if discovery fails

---

## 🧠 Embedding Model Setup

Place model files here:

```
app/src/main/assets/models/
```

Required:

* `all-minilm-l6-v2.onnx`
* `vocab.txt`

---

## 🔍 RAG System

### Edge (On-device)

* Fast
* Uses local embeddings
* Searches:

  * Event logs
  * Documents
  * Entity facts

### PC RAG

* Used when confidence is low
* Handles:

  * Deep queries
  * External knowledge
  * Web search

---

## 🎯 Key Components

### Android

* `EdgeRAGEngine` → local retrieval
* `EmbeddingEngine` → vector generation
* `PCDiscovery` → finds server
* `VoiceCommandProcessor` → intent parsing
* `ExplicitRagIntent` → query routing logic

---

### PC

* FastAPI server
* Handles heavy AI tasks
* Provides endpoints for mobile app

---

## 🧪 Testing

### PC

Open browser:

```
https://localhost:8472/docs
```

### Android

* Run app on device
* Trigger voice / actions
* Check logs in Logcat

---

## ⚠️ Common Issues

### 1. Server not starting

* Check SSL paths
* Verify cert files exist

### 2. Gradle errors

* Use correct versions:

  * Gradle 8.4+
  * AGP 8.2.2

### 3. Unresolved references

* Missing enums (`QueryType`, `RetrievalLayer`)
* Wrong package names

### 4. PC not discovered

* Ensure same WiFi network
* Check firewall

---

## 🔮 Future Improvements

* Replace in-memory vector store with FAISS / sqlite-vss
* Add offline LLM on device
* Improve intent detection
* UI for memory visualization

---

## 👨‍💻 Author

Built as a personal AI system project combining:

* Mobile AI
* Edge computing
* Distributed intelligence

---

## 📜 License

This project is for learning and experimentation.
