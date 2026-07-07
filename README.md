# LLM Corso

Corso-gioco interattivo (IT/EN) sulla meccanica interna degli LLM. Zero dipendenze, zero build.

## Modulo 1 — Dentro l'inferenza (`index.html`)

Token, attention (Q/K/V), layer e MLP, KV cache, formula della memoria, budget VRAM,
prefix caching, eviction. 7 capitoli + test a punti.

## Modulo 2 — Memoria e RAG (`modulo2/index.html`)

Tipi di memoria di un LLM (parametrica, contesto, esterna/RAG, conversazionale), limiti
della context window, embedding, chunking, retrieval e reranking. 7 capitoli + test a punti.

Ogni capitolo può essere letto senza fare il test (pulsante "solo lettura" → capitolo
successivo); i due moduli sono linkati tra loro dalle rispettive home.

**Demo locale:** apri `index.html` (Modulo 1) o `modulo2/index.html` (Modulo 2) in un browser.

**Deploy:** file statici — GitHub Pages, Netlify, Vercel o un qualsiasi web server.
