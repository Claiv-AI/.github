<div align="center">

<img src="https://claiv.io/claiv-logo-96.png" width="72" height="72" alt="Claiv" />

# Claiv

**Software for AI that has to account for itself.**

[claiv.io](https://claiv.io) · [How this got here](https://claiv.io/about) · [Docs](https://claiv.io/docs)

[![LoCoMo J-Score](https://img.shields.io/badge/LoCoMo%20J--Score-75.0%25-brightgreen)](https://claiv.io/about)
[![SDK: JavaScript](https://img.shields.io/badge/SDK-JavaScript-yellow)](https://github.com/Claiv-Memory/sdk-js)
[![SDK: Python](https://img.shields.io/badge/SDK-Python-blue)](https://github.com/Claiv-Memory/sdk-py)

</div>

---

Three products, built in that order, each the answer to a problem the last one
exposed. The full account is at [claiv.io/about](https://claiv.io/about).

## CLAIV Studio

**An AI organisation you can govern.** Describe an outcome and Studio designs a
team of specialists around it — their knowledge, their connections and their
limits set out before any of it exists. You approve the design. It builds the
specialists and proves them against realistic cases. Then it runs, and every
decision, authority and verified effect is on the record.

- Authority is explicit per specialist
- Approval is bound to the exact action, not to a category
- Effects are verified against the system itself, not assumed from an approval
- Credentials are handles, never values
- Runs on your own computer, and can run models locally

Windows, in paid early access. **[Request access →](https://claiv.io/early-access)**
The download and every release note live on your
[account page](https://claiv.io/account).

## CLAIV Memory

**A persistent memory API.** Your AI forgets everything between sessions;
context windows only move the ceiling. Memory gives it continuity:

- Persistent user memory across conversations
- Document understanding, not just chunk retrieval
- Temporal awareness — what happened, and when
- Context injection ready for an LLM prompt
- Controlled forgetting, for when someone asks to be deleted

```http
POST /v6/ingest      →  store memory events
POST /v6/recall      →  retrieve context
POST /v6/documents   →  upload documents
POST /v6/forget      →  delete memory
```

**Python**

```bash
pip install claiv-memory
```

```python
from claiv import ClaivClient

client = ClaivClient(api_key="your_key")

client.ingest({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "type": "message",
    "role": "user",
    "content": "I'm building an AI agent for compliance review.",
})

context = client.recall({
    "user_id": "user_123",
    "conversation_id": "conv_abc",
    "query": "What is the user building?",
})

print(context["llm_context"]["text"])   # inject into your system prompt
```

**JavaScript / TypeScript**

```bash
npm install @claiv/memory
```

```javascript
import { ClaivClient } from '@claiv/memory';

const client = new ClaivClient({ apiKey: 'your_key' });
await client.ingest({ user_id: 'user_123', conversation_id: 'conv_abc',
  type: 'message', role: 'user', content: "I'm building an AI agent." });
const context = await client.recall({ user_id: 'user_123',
  conversation_id: 'conv_abc', query: 'What is the user building?' });
```

### Benchmark

Official LoCoMo result across all ten dialogues — the standard benchmark for
long-conversation memory:

| Overall J-score | Open domain | Temporal | Single hop | Multi hop |
|:---:|:---:|:---:|:---:|:---:|
| **75.0%** | 79.7% | 74.2% | 68.8% | 55.2% |

### Notes that save an afternoon

- Ingest is asynchronous — memory may not appear instantly
- Always include `user_id` and `conversation_id`
- Inject `llm_context.text` into your system prompt, not the raw events
- API key authentication with tenant isolation; deletion is scoped via `/v6/forget`

Version 6.3, in production at `api.claiv.io`. **Available on request** rather
than self-service sign-up — [read the docs](https://claiv.io/docs), then write
to `support@claiv.io` and we will set up a project and issue a key.

## Claiv Parser

**Deterministic structured output, with no model.** Every system that asks an
LLM for JSON eventually writes half a parser to cope with what comes back:
fenced blocks, chatty preambles, Python `True`, truncation — and search models
that return prose with citations and no JSON at all.

Six tiers run cheapest-first and stop at the first schema-valid result. Tiers
0–4 are pure functions, so the same input and schema give byte-identical output
every time, offline. It never invents: anything absent from the source is
`null` and listed in `unresolved`, and every field reports how it was resolved
— exact, repaired, coerced, or read from markdown.

```bash
npm install @claiv/parser
```

MIT, zero-dependency · [npm](https://www.npmjs.com/package/@claiv/parser)

---

## Repositories

| Repo | What it is |
|---|---|
| [sdk-js](https://github.com/Claiv-Memory/sdk-js) | JavaScript / TypeScript SDK for the Memory API |
| [sdk-py](https://github.com/Claiv-Memory/sdk-py) | Python SDK for the Memory API |
| [claiv-memory](https://github.com/Claiv-Memory/claiv-memory) | The memory layer itself |
| [ai-chatbot-with-memory](https://github.com/Claiv-Memory/ai-chatbot-with-memory) | A chatbot that remembers users across sessions |
| [Claiv-Studio-Releases](https://github.com/Claiv-Memory/Claiv-Studio-Releases) | CLAIV Studio builds and release notes |

---

<div align="center">
<sub>Access requests, questions and bug reports: <a href="mailto:support@claiv.io">support@claiv.io</a></sub>
</div>
