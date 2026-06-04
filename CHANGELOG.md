# Changelog

Tutte le modifiche notabili a questo progetto sono documentate qui.

## v4.2.1 — 2026-06-04 (beta)

### `verifica-fonti` — integrazione BuddaLaw MCP

La skill `verifica-fonti` ora supporta il connettore BuddaLaw MCP come **fonte
giurisprudenziale italiana opzionale**, con due regole:

1. **Solo se l'avvocato ce l'ha già**. Se nella sessione è disponibile il
   connettore BuddaLaw e l'avvocato lo ha autorizzato in allowlist, la skill
   può interrogarlo. Chi non ha BuddaLaw non vede cambiamenti: la skill
   continua a usare gli stessi registri web di prima (Italgiure CED via Chrome
   MCP, Normattiva, EUR-Lex, ecc.).
2. **Consenso esplicito al primo uso della sessione**. Anche se l'avvocato ha
   BuddaLaw configurato, la skill avvisa la prima volta della sessione che sta
   per instradare la query verso il connettore e chiede conferma. Niente uso
   silenzioso. Su rifiuto: la skill prosegue con i registri web come prima.

### Integrazione tecnica

L'abbonamento BuddaLaw resta dell'avvocato. BeccarIA non ha alcun rapporto
commerciale con BuddaLaw: è una segnalazione tecnica di compatibilità via
protocollo MCP. Se BuddaLaw non trova risultati o restituisce errore/timeout,
la skill esegue automaticamente fallback ai registri web standard senza
chiedere conferma.

### Stato di maturità

Siamo in **beta**. Il pezzo "la skill usa BuddaLaw + fallback web" è stato
validato da un tester (Giuseppe Girlando) con esito positivo su flusso
reale. Il pezzo "la skill chiede consenso al primo uso" (il consent-gate) è
stato scritto e dovrebbe comportarsi come descritto, ma non è ancora stato
osservato all'opera su un avvocato che parte da zero. Se la skill chiede male,
chiede dove non dovrebbe, o non chiede dove dovrebbe — scrivetecelo (via
issue su GitHub o nel gruppo Giuristi AI).

### Allineamento cross-repo

Questa release allinea il plugin standalone `beccaria-solo-controllo-fonti` alla
versione `4.2.1` del plugin BeccarIA completo (`MicheleLoi/legal-tech-cowork`).
La numerazione di versione segue d'ora in avanti quella del repo principale per
mantenere riconoscibile la parità della skill `verifica-fonti` (salto da v1.0.0
del primo rilascio standalone a v4.2.1 per allineamento cross-repo).

Lo scope del plugin standalone resta invariato: **solo la skill
`verifica-fonti`**, nessun bollettino RegIA, nessun catalogo dinamico, nessun
fetch a `bulletins.micheleloi.pro`. Vedi `README.md` per la differenza
sostanziale con BeccarIA completo.

## v1.0.0 — 2026-05-26

Rilascio iniziale del plugin standalone `beccaria-solo-controllo-fonti`:
singola skill `verifica-fonti` per controllo coerenza citazioni normative
italiane ed europee, senza dipendenza da bollettino RegIA. Vedi commit
`6496c0d` per dettaglio.
