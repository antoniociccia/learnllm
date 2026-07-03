# LLM Corso — Corso interattivo sugli LLM

## Cos'è
Corso-gioco statico (HTML singolo, zero dipendenze, zero build) sulla meccanica interna degli LLM.
Modulo 1: "Dentro l'inferenza" (token, attention Q/K/V, KV cache, formula memoria, budget VRAM, prefix caching, eviction).
Formato: capitolo di lettura (2-3 min) → test a punti, per 7 capitoli (0-6). Grado finale + share LinkedIn.

## Struttura
- `index.html` — tutto il Modulo 1: CSS + markup + JS + contenuti. Nessun asset esterno tranne Google Fonts.
- Nessun framework, nessun bundler, nessun localStorage (stato solo in memoria, per compatibilità).

## Architettura interna (index.html)
- **i18n**: tutto il contenuto vive nell'oggetto `I18N = { it: {...}, en: {...} }`.
  Ogni lingua ha le chiavi: `ui` (stringhe interfaccia, rank, share), `gloss` (glossario),
  `ch0` (capitolo 0), `ch` (array capitoli 1-6, `{title, body}` con body in HTML),
  `l1`, `l2`, `l5`, `boss` (quiz), `l4` (blocchi ordinamento).
  Il selettore lingua si genera automaticamente da `Object.keys(I18N)`.
- **Motore**: `build()` costruisce `LEVELS` dalla lingua attiva; `R` traccia la route corrente
  (home/gloss/chapter/test/final) così il cambio lingua ri-renderizza senza perdere il punteggio `S`.
- **Livelli**: quiz generico (`quizQ`), simulatore VRAM (`simRun`, formula 2×32×k×d×c, pesi 8×w GB su 24 GB),
  ordinamento contesto (`orderRun`), boss a tempo (`timed:12`).
- **Punteggio**: base 100 (150 timed, 300 sim/order) × (1 + streak×0.15). Rank per percentuale sul massimo.

## Convenzioni per estendere
- **Nuova lingua**: aggiungere una chiave a `I18N` con TUTTE le stesse sotto-chiavi di `it`. Niente altro.
- **Modulo 2 (memoria e RAG, pianificato)**: creare `modulo2/index.html` clonando la struttura;
  la home del Modulo 1 già annuncia i moduli futuri. Valutare una landing `index` comune se i moduli diventano 2+.
- **Nuovi capitoli nel modulo**: aggiungere elemento a `ch[]` (entrambe le lingue) + livello in `build()`.
- Verifica sintassi JS dopo ogni modifica: estrarre lo script e `node --check`.
- Mantenere: niente localStorage/sessionStorage, un solo file per modulo, contenuti sempre in entrambe le lingue.

## Deploy
Statico puro: GitHub Pages, Netlify, Vercel o qualsiasi web server. Nessuna build necessaria.
GitHub Pages (consigliato): repo pubblico → Settings → Pages → deploy from branch `main`, root.
