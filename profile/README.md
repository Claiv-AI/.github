# 🧠 CLAIV Memory

**AI Memory for Chatbots, Agents, and LLM Apps**

> Your AI forgets everything.
> CLAIV fixes that.

[![LoCoMo J-Score](https://img.shields.io/badge/LoCoMo%20J--Score-75.0%25-brightgreen)](https://claiv.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![SDK: JavaScript](https://img.shields.io/badge/SDK-JavaScript-yellow)](https://github.com/Claiv-Memory/sdk-js)
[![SDK: Python](https://img.shields.io/badge/SDK-Python-blue)](https://github.com/Claiv-Memory/sdk-py)

---

## 🚨 The problem

If you're building with OpenAI, Claude, or LangChain — you've seen this:

- Your chatbot forgets users between sessions
- Your AI agent loses context after a few steps
- Your app relies on fragile chat history or prompt stuffing
- Your RAG setup is inconsistent and unreliable

👉 This is not a model problem — it's a **memory problem**

---

## ✅ The solution

CLAIV is a **drop-in memory API for AI applications.**

It gives your AI:

- 🧠 **Persistent user memory** across conversations
- 📚 **Reliable document understanding** (not just chunk retrieval)
- ⏱️ **Temporal awareness** — what happened and when
- 🎯 **Context injection** ready for LLM prompts
- 🧹 **Controlled forgetting** — GDPR-safe deletion

---

## ⚡ What this looks like

**❌ Without memory**

```
User:  My name is Alex and I run a fitness business.

...later...

AI:    How can I help you today?
```

**✅ With CLAIV**

```
AI:    How is your fitness business going, Alex?
```

---

## 🛠️ How it works

1. Send events to `POST /v6/ingest`
2. CLAIV extracts structured memory asynchronously
3. Call `POST /v6/recall` before each LLM response
4. Inject `llm_context.text` into your system prompt

That's it.

---

## 🚀 Quickstart

### 1. Install

```bash
pip install claiv-memory
```

### 2. Store memory

```python
from claiv import ClaivClient

client = ClaivClient(api_key="your_key")

client.ingest({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "type": "message",
    "role": "user",
    "content": "I'm building an AI agent for compliance review."
})
```

### 3. Recall memory

```python
context = client.recall({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "query": "What is the user building?"
})

print(context["llm_context"]["text"])
```

### 4. Inject into your LLM

```
System prompt:

User memory:
{{ llm_context.text }}
```

**JavaScript / TypeScript**

```bash
npm install @claiv/memory
```

```javascript
import { ClaivClient } from '@claiv/memory';

const client = new ClaivClient({ apiKey: 'your_key' });

await client.ingest({
  user_id: 'user_123',
  conversation_id: 'conv_abc',
  type: 'message',
  role: 'user',
  content: "I'm building an AI agent for compliance review.",
});

const context = await client.recall({
  user_id: 'user_123',
  conversation_id: 'conv_abc',
  query: 'What is the user building?',
});
```

---

## 📄 Document memory (built-in RAG)

Upload documents and CLAIV will:

- Parse structure into sections and spans
- Embed content with pgvector
- Retrieve relevant sections automatically
- Inject them into your LLM context

```python
doc = client.upload_document({
    "user_id": "user_123",
    "project_id": "proj_abc",
    "document_name": "Product Manual",
    "content": open("manual.md").read(),
})

print(f"Indexed {doc['spans_created']} spans across {len(doc['sections'])} sections")
```

Supports:

- Knowledge copilots over internal documentation
- Compliance and research tools
- Support assistants that reason over policies and manuals

---

## 🧠 What makes CLAIV different

| Feature | Vector DB | CLAIV |
|---|---|---|
| Remembers users over time | ❌ | ✅ |
| Structured fact extraction | ❌ | ✅ |
| Temporal reasoning | ❌ | ✅ |
| Token-efficient recall | ❌ | ✅ |
| Document + conversation memory | ❌ | ✅ |
| Controlled forgetting | ❌ | ✅ |

---

## ⚙️ API

```http
POST /v6/ingest      →  Store memory events
POST /v6/recall      →  Retrieve context
POST /v6/documents   →  Upload documents
POST /v6/forget      →  Delete memory
```

Full reference → [claiv.io/docs](https://claiv.io/docs)

---

## 🧪 Benchmark

**LoCoMo 10-dialogue J-score: 75.0%**

| Category | Score |
|---|---|
| Single-hop | 68.8% |
| Temporal | 74.2% |
| Multi-hop | 55.2% |
| Open-domain | 79.7% |

LoCoMo is the standard benchmark for long-context conversational memory in production AI systems.

---

## 🧩 Use cases

- AI chatbots with persistent memory
- AI agents with multi-step workflows
- SaaS apps with per-user context
- Customer support systems
- Internal knowledge copilots
- Research and compliance tools

---

## ⚠️ Notes

- Ingest is async — memory may not appear instantly
- Always include `user_id` and `conversation_id`
- Inject `llm_context.text` into your system prompt

---

## 🔐 Security

- API key authentication with tenant isolation
- Strict schema validation on all endpoints
- Scoped deletion via `POST /v6/forget`

---

## 📦 Repositories

| Repo | Description |
|---|---|
| [sdk-js](https://github.com/Claiv-Memory/sdk-js) | JavaScript / TypeScript SDK |
| [sdk-py](https://github.com/Claiv-Memory/sdk-py) | Python SDK |
| [template-openai-nodejs](https://github.com/Claiv-Memory/template-openai-nodejs) | OpenAI Node.js template |
| [template-openai-python](https://github.com/Claiv-Memory/template-openai-python) | OpenAI Python template |
| [template-claude-python](https://github.com/Claiv-Memory/template-claude-python) | Claude template |
| [template-langchain](https://github.com/Claiv-Memory/template-langchain) | LangChain template |
| [template-nextjs](https://github.com/Claiv-Memory/template-nextjs) | Next.js chat app |
| [template-document-rag-python](https://github.com/Claiv-Memory/template-document-rag-python) | Document RAG (Python) |
| [template-document-rag-nextjs](https://github.com/Claiv-Memory/template-document-rag-nextjs) | Document RAG (Next.js) |

---

## 🚀 Get started

👉 **Get API key:** [claiv.io](https://claiv.io)

👉 **Docs:** [claiv.io/docs](https://claiv.io/docs)
