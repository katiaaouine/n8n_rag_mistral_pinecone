## n8n AI RAG Chatbot (Mistral + Pinecone)
Un workflow n8n permettant de créer un chatbot intelligent basé sur tes documents (RAG - Retrieval Augmented Generation).

##Objectif du projet:
- connecter n8n avec un LLM (Mistral)
- indexer des données dans Pinecone
- créer un agent capable de répondre à partir de documents personalisés
  
ce projet peut etre utilisé par :
- chatbot interne entreprise
- assistant documentaire
- FAQ automatisée


 ## Fonctionnalités
-  Upload et extraction de fichiers (Google Drive)
-  Embedding avec Mistral
- Stockage vectoriel via Pinecone
-  Chatbot avec agent AI
-  Recherche sémantique (RAG)

##  Stack technique:
- n8n (automation)
- Mistral API (LLM)
- Pinecone (vector database)
- Langchain nodes
- Google Drive API

##  Contenu du repo
- `workflow.json` → workflow n8n importable
- `.env.example` → variables d’environnement à configurer

---

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











