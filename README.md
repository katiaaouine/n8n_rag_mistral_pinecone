<img width="1797" height="818" alt="Screenshot 2026-06-03 11 32 26" src="https://github.com/user-attachments/assets/5662cb71-e1e3-44f2-8e47-8a36423eea52" />

#  AI RAG Chatbot — n8n · Mistral · Pinecone

<div align="center">

![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Mistral AI](https://img.shields.io/badge/Mistral_AI-FF7000?style=for-the-badge&logoColor=white)
![Pinecone](https://img.shields.io/badge/Pinecone-000000?style=for-the-badge&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logoColor=white)
![License MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Système RAG no-code production-ready — recherche sémantique & génération contextuelle sur documents personnalisés**

 [Installation](#-installation) · [Architecture](#️-architecture) 

</div>

---

##  Vue d'ensemble

Ce projet implémente un **pipeline RAG (Retrieval-Augmented Generation) complet** orchestré sans backend via n8n. Il permet d'interroger en langage naturel un corpus de documents personnalisés — ici un dataset COVID-19 — en obtenant des réponses précises, contextualisées et **sans hallucination**.

>  L'architecture est générique : remplace le dataset COVID par n'importe quelle base documentaire (RH, juridique, support, finance...).

---

##  Features

###  Pipeline d'ingestion (one-shot)
- **Import automatique** depuis Google Drive (CSV, PDF, documents)
- **Chunking intelligent** via Recursive Character Text Splitter (chunk: 500 tokens, overlap: 50 )
- **Génération d'embeddings** avec le modèle `mistral-embed` (vecteurs 1024 dimensions)
- **Indexation vectorielle** dans Pinecone avec namespace dédié

###  Pipeline conversationnel (temps réel)
- **Agent LangChain** avec system prompt anti-hallucination strict
- **Pinecone en mode `retrieve-as-tool`** — architecture agent avancée (pas un simple retriever)
- **Mistral Large** pour la génération de réponses contextuelles
- **Réponses sourcées** exclusivement sur les documents indexés
- **Interface chat** intégrée n8n, activable via webhook

###  Bonnes pratiques
- Secrets protégés via `.env.example` + `.gitignore`
- Workflow exportable et importable en un clic (`rag_workflow.json`)
- Stack 100% européenne (Mistral AI) — **compatible RGPD**
- Architecture découplée : ingestion et chat sont deux workflows indépendants

---

##  Architecture
---

Flux résumé :
  Ingestion : Document ──▶ Chunks ──▶ Vectors ──▶ Pinecone
  Chat      : Question ──▶ Vector ──▶ Top-K chunks ──▶ Mistral ──▶ Réponse
```

---

## Stack technique

| Outil | Rôle |
|---|---|
| **n8n** | Orchestration no-code du pipeline complet |
| **Mistral AI** `mistral-embed` | Génération des embeddings (1024 dimensions) |
| **Mistral AI** `mistral-large-latest` | Génération des réponses LLM |
| **Pinecone** | Base vectorielle serverless — indexation & recherche sémantique |
| **LangChain nodes** | AI Agent, Vector Store Tool, Recursive Text Splitter |
| **Google Drive API** | Source des documents à ingérer |

---

##  Structure du repo

```
n8n_rag_mistral_pinecone/
│
├── 📁 data/
│   └── covid_data.csv           # Dataset COVID-19 (exemple)
│
├── rag_workflow.json             # Workflow n8n importable en 1 clic
├── .env.example                  # Template des variables d'environnement
├── .gitignore                    # Protection des secrets
└── README.md
```

---

##  Installation

### Prérequis

- ✅ [n8n](https://n8n.io) installé — local (`npm install -g n8n`) ou cloud
- ✅ Compte [Mistral AI](https://console.mistral.ai) + clé API
- ✅ Compte [Pinecone](https://app.pinecone.io) + index créé
- ✅ Projet [Google Cloud](https://console.cloud.google.com) avec Drive API activée

### Étape 1 — Cloner le repo

```bash
git clone https://github.com/katiaaouine/n8n_rag_mistral_pinecone.git
cd n8n_rag_mistral_pinecone
```

### Étape 2 — Configurer les variables d'environnement

```bash
cp .env.example .env
```

Édite `.env` avec tes vraies clés :

```env
MISTRAL_API_KEY="sk-..."          # console.mistral.ai
PINECONE_API_KEY="pcsk_..."       # app.pinecone.io
GOOGLE_DRIVE_CREDENTIALS="..."    # console.cloud.google.com
```

### Étape 3 — Créer l'index Pinecone

Dans [app.pinecone.io](https://app.pinecone.io), crée un index avec ces paramètres :

| Paramètre | Valeur |
|---|---|
| Name | `covidrag` |
| Dimensions | `1024` (mistral-embed) |
| Metric | `cosine` |
| Type | Serverless |

### Étape 4 — Importer le workflow dans n8n

1. Lance n8n : `npx n8n`
2. **Workflows** → **Import from file** → sélectionne `rag_workflow.json`
3. Configure les 3 credentials :
   - `Mistral Cloud account` → Mistral API key
   - `Pinecone account` → Pinecone API key
   - `Google Drive OAuth2 API` → authentification Google

### Étape 5 — Lancer l'ingestion

1. Ouvre le workflow dans n8n
2. Clique sur **Execute workflow** (pipeline d'ingestion)
3. Vérifie dans Pinecone que les vecteurs apparaissent dans l'index `covidrag`

### Étape 6 — Démarrer le chat

1. Active le workflow (toggle **Active** → ON)
2. Ouvre le **Chat** intégré n8n
3. Pose ta question — l'agent répond uniquement sur les données indexées 

---

##  Cas d'usage — Dataset COVID-19

Le projet utilise un dataset COVID-19 (cas, décès, vaccinations par pays). 

---
> L'agent répond **uniquement sur les données indexées**, sans inventer de chiffres.



---

## Auteure

**Katia Aouine** — AI Engineer

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Katia_Aouine-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/katia-aouine/)
[![GitHub](https://img.shields.io/badge/GitHub-katiaaouine-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/katiaaouine)

---

<div align="center">
  <sub>Built  using n8n · Mistral AI · Pinecone</sub>
</div>











