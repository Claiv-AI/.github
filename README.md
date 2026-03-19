<div align="center">

# CLAIV Memory

### Persistent memory infrastructure for AI applications

[![LoCoMo J-Score](https://img.shields.io/badge/LoCoMo%20J--Score-75.0%25-brightgreen)](https://claiv.io/benchmarks/locomo)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![SDK: JavaScript](https://img.shields.io/badge/SDK-JavaScript-yellow)](https://github.com/Claiv-Memory/sdk-js)
[![SDK: Python](https://img.shields.io/badge/SDK-Python-blue)](https://github.com/Claiv-Memory/sdk-py)

**Store events. Ingest documents. Recall relevant context. Forget intentionally.**

[Get Started](https://claiv.io) · [Read the Docs](https://claiv.io/docs) · [Templates](#repositories)

</div>

---

## What CLAIV Memory is

CLAIV Memory is a production memory system for AI applications. It gives agents and applications the ability to store events, upload documents, retrieve relevant context, and delete data intentionally — with APIs built for real-world use.

This is not chat history or basic vector search. It is a dedicated memory layer that supports:

- **Event memory** — structured facts extracted from interactions over time
- **Document memory** — uploaded files indexed for recall, not dead attachments
- **Contextual recall** — surface relevant memory from either source at the right moment
- **Controlled forgetting** — delete or suppress data when it should no longer be retained

---

## Why it exists

Most AI apps still break in the same places:

- They forget important user details between sessions
- They lose track of prior decisions and context
- They cannot reliably use uploaded documents over time
- They struggle to remove data cleanly when required
- They depend on fragile prompt stuffing or naive retrieval

CLAIV Memory is built to solve that. Plug it into your product and your assistant, copilot, or agent can remember what matters — across conversations and documents.

---

## Benchmark

**LoCoMo 10-dialogue J-score: 75.0%**

| Category | Score |
|---|---|
| Single-hop | 68.8% |
| Temporal | 74.2% |
| Multi-hop | 55.2% |
| Open-domain | 79.7% |

LoCoMo is the standard benchmark for long-context conversational memory in production AI systems.

---

## Why CLAIV over a vector database

| Feature | Vector DB | CLAIV Memory |
|---|---|---|
| Retrieval type | Similarity search | Structured, deterministic facts |
| Contradiction handling | ❌ | ✅ Resolved automatically |
| Token budget management | ❌ | ✅ Built-in ranked recall |
| GDPR deletion proof | ❌ | ✅ Timestamped audit receipt |
| Evidence-backed facts | ❌ | ✅ Character-exact source quotes |
| Temporal tracking | ❌ | ✅ Fact version history |
| Document memory | ❌ | ✅ First-class, indexed for recall |

---

## API surface

Four core endpoints cover the full memory lifecycle:

```http
POST /v6/ingest      →  Store a memory event from a conversation
POST /v6/documents   →  Upload and index a document for recall
POST /v6/recall      →  Retrieve ranked context from events and documents
POST /v6/forget      →  Delete user data with a timestamped audit receipt
```

Health check (no auth required):

```http
GET /healthz  →  { "ok": true }
```

---

## Quick start (Python)

```bash
pip install claiv-memory
```

```python
from claiv import ClaivClient

client = ClaivClient(api_key="your_key")

# Store a memory event
client.ingest({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "type": "conversation",
    "role": "user",
    "content": "I'm building an AI agent for compliance review.",
})

# Recall relevant context for the next turn
context = client.recall({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "query": "What is the user building?",
})

system_prompt = f"User context:\n{context['llm_context']['text']}"

# Upload a document into memory
doc = client.upload_document({
    "user_id": "user_123",
    "project_id": "proj_abc",
    "document_name": "Product Manual",
    "content": open("manual.md").read(),
})
# doc["spans_created"] → number of indexed spans
# doc["status"]        → "processing" (distillations complete async)

# Forget a user's data
client.forget({
    "user_id": "user_123",
})
```

## Quick start (JavaScript)

```bash
npm install @claiv/memory
```

```javascript
import { ClaivClient } from '@claiv/memory';

const client = new ClaivClient({ apiKey: 'your_key' });

// Store a memory event
await client.ingest({
  user_id: 'user_123',
  conversation_id: 'conv_abc',
  type: 'conversation',
  role: 'user',
  content: "I'm building an AI agent for compliance review.",
});

// Recall relevant context
const context = await client.recall({
  user_id: 'user_123',
  conversation_id: 'conv_abc',
  query: 'What is the user building?',
});

// Upload a document
const doc = await client.uploadDocument({
  user_id: 'user_123',
  project_id: 'proj_abc',
  document_name: 'Product Manual',
  content: manualText,
});
```

---

## Document memory

Document ingest is a first-class part of CLAIV Memory, not an add-on.

Uploaded documents are parsed into sections and spans, indexed for retrieval, and surfaced during recall when relevant — alongside event memory. This enables:

- Knowledge copilots over internal documentation
- Due diligence and research assistants
- Compliance and evidence retrieval systems
- Support tools that reason over manuals and policies
- Agents that combine long-term event memory with file-based context

---

## Use cases

CLAIV Memory is well suited to products that need reliable context over time:

- AI assistants with persistent user memory
- Customer support systems
- Internal knowledge copilots
- Legal and compliance research tools
- Enterprise search with memory
- Workflow agents that need continuity across sessions
- Products that combine conversation context with uploaded files

---

## Works with

- ✅ OpenAI
- ✅ Anthropic Claude
- ✅ LangChain
- ✅ Any LLM with a system prompt

---

## Repositories

| Repo | Description |
|---|---|
| [sdk-js](https://github.com/Claiv-Memory/sdk-js) | JavaScript / TypeScript SDK |
| [sdk-py](https://github.com/Claiv-Memory/sdk-py) | Python SDK |
| [template-openai-nodejs](https://github.com/Claiv-Memory/template-openai-nodejs) | OpenAI Node.js integration |
| [template-openai-python](https://github.com/Claiv-Memory/template-openai-python) | OpenAI Python integration |
| [template-claude-python](https://github.com/Claiv-Memory/template-claude-python) | Anthropic Claude integration |
| [template-langchain](https://github.com/Claiv-Memory/template-langchain) | LangChain integration |
| [template-nextjs](https://github.com/Claiv-Memory/template-nextjs) | Next.js chat app |
| [template-document-rag-python](https://github.com/Claiv-Memory/template-document-rag-python) | Document RAG (Python) |
| [template-document-rag-nextjs](https://github.com/Claiv-Memory/template-document-rag-nextjs) | Document RAG (Next.js) |

---

<div align="center">

CLAIV Memory gives AI systems durable memory across events and documents — with retrieval and forgetting built in.

[claiv.io](https://claiv.io) · [Get your API key](https://claiv.io) · [Documentation](https://claiv.io/docs)

</div>
