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

### 1. Crea un account su JSONBin
https://jsonbin.io → Registrati gratis

### 2. Crea un Bin
- Vai su "Bins" → "Create Bin"
- Inserisci come contenuto iniziale:
  ```json
  { "proposals": [], "votes": [] }
  ```
- Clicca "Create"
- Copia il **BIN ID** dalla URL (es. `6650abc123def456`)

### 3. Ottieni la Master Key
- Vai su "API Keys" nel tuo account
- Copia la **Master Key** (inizia con `$2a$10$...`)

### 4. Aggiorna config.js
```js
const CONFIG = {
  JSONBIN_MASTER_KEY: '$2a$10$XXXXXXXXXXXXXXXXXX',  // ← la tua
  BIN_ID:             '6650XXXXXXXXXXXXXXXX',         // ← il tuo
  TOTAL_VOTERS: 6,  // ← quante persone voteranno
};
```

### 5. Carica su GitHub Pages
- Crea una repo GitHub pubblica
- Carica tutti i file (index.html, vote.html, style.css, config.js)
- Vai su Settings → Pages → Source: main branch
- Il link sarà: `https://tuousername.github.io/nome-repo/`

---

## Struttura file

```
├── config.js      → credenziali JSONBin + numero votanti
├── style.css      → stili condivisi
├── index.html     → pagina proposta mete
└── vote.html      → pagina voto + risultati
```

---

## Note importanti

- **Sicurezza**: la Master Key è visibile nel codice. Per un sondaggio tra amici è accettabile; non usare per dati sensibili.
- **Reset**: per ricominciare da zero, apri JSONBin e resetta il bin a `{ "proposals": [], "votes": [] }`.
- **Doppio voto**: il sistema controlla il nome lato server (JSONBin). Il localStorage aggiunge solo un layer UX locale.
- **Race condition**: in caso rarissimo di submit simultaneo da due persone nello stesso istante, un voto potrebbe sovrapporsi. Per un gruppo piccolo è trascurabile.
