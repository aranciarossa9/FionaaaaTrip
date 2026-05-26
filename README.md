# FIONAAAAA's TRIP 🌍✈️

Sondaggio per scegliere la meta del viaggio di gruppo in stile pesato 3-2-1.

---

## Come funziona

**index.html — Proponi**
Ogni partecipante inserisce il suo nome e 3 mete preferite, ognuna con:
- Città di destinazione
- Periodo preferito (ottobre / novembre, con granularità)
- Note motivazionali (perché andarci)

I punteggi sono automatici: 1ª meta = 3 punti, 2ª = 2 punti, 3ª = 1 punto.
Una volta inviato, la pagina ricorda che hai già proposto (localStorage).

**vote.html — Vota**
Mostra tutte le destinazioni proposte da tutti i partecipanti, deduplicate per città.
Ogni votante seleziona le sue 3 preferite cliccando in ordine (1° → 2° → 3°).
Il punteggio si calcola automaticamente al momento del submit.

I risultati restano nascosti fino a quando **tutti i votanti previsti** hanno votato.
Quando il contatore raggiunge TOTAL_VOTERS, la classifica si svela automaticamente.

---

## Setup (5 minuti)

### 1. Usa l'endpoint npoint fornito
Non servono login né API key.

### 2. Aggiorna config.js
```js
const CONFIG = {
  DATA_URL: 'https://api.npoint.io/631ab5e192ef75b1820e',
  VOTING_START_DATE: '2026-05-24T00:00:00',
  TOTAL_VOTERS: 6,  // ← quante persone voteranno
};
```

### 3. Carica su GitHub Pages
- Crea una repo GitHub pubblica
- Carica tutti i file (index.html, vote.html, style.css, config.js)
- Vai su Settings → Pages → Source: main branch
- Il link sarà: `https://tuousername.github.io/nome-repo/`

---

## Struttura file

```
├── config.js      → URL npoint + numero votanti
├── style.css      → stili condivisi
├── index.html     → pagina proposta mete
└── vote.html      → pagina voto + risultati
```

---

## Note importanti

- **Storage**: l'app ora usa npoint come backend JSON.
- **Reset**: per ricominciare da zero, apri il bin npoint e resetta i dati a `{ "proposals": [], "votes": [] }`.
- **Doppio voto**: il sistema controlla il nome lato server. Il localStorage aggiunge solo un layer UX locale.
- **Race condition**: in caso rarissimo di submit simultaneo da due persone nello stesso istante, un voto potrebbe sovrapporsi. Per un gruppo piccolo è trascurabile.
