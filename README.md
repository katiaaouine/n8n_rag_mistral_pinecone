<img width="1699" height="648" alt="Screenshot 2026-06-02 11 01 01" src="https://github.com/user-attachments/assets/a35aad9d-c2f0-44bb-be16-5a44cf11bead" />

#  AI RAG Chatbot (n8n • Mistral • Pinecone)

Système RAG ,conçu avec un pipeline no-code permettant une recherche sémantique et la génération de réponses contextuelles à partir de documents personnalisés.

##  Fonctionnalités

- Pipeline RAG complet : ingestion → embeddings → retrieval → génération  
- Recherche sémantique via base vectorielle Pinecone  
- Intégration d’un LLM (Mistral) pour des réponses fiables et contextualisées  
- Automatisation du workflow avec n8n  

##  Architecture

Documents → Chunking → Embeddings → Vector DB → Retrieval → LLM → Réponse  

##  Objectif
Démontrer la conception d’un système d’IA générative scalable combinant LLM, vector search et automatisation pour construire un moteur de connaissance intelligent.

##  Stack technique:

- n8n (automation)
- Mistral API (LLM)
- Pinecone (vector database)
- Langchain nodes
- Google Drive API

##  Contenu du repo

- `workflow.json` → workflow n8n importable
- `.env.example` → variables d’environnement à configurer

##  Installation

### 1. Installer n8n
- Local ou cloud

### 2. Importer le workflow
- Ouvre n8n
- Clique sur "Import"
- Upload `workflow.json`

### 3. Configurer les credentials
Tu devras ajouter :
- Mistral API key
- Pinecone API key
- Google Drive credentials

##  Utilisation
1. Upload un fichier (CSV / documents)
2. Le workflow indexe les données
3. Pose une question via le chatbot
4. L’agent répond à partir des données











