# BeccarIA — solo controllo fonti

[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

Plugin Claude Code marketplace con una **sola skill** — `verifica-fonti` — pensata per l'avvocato italiano che vuole un controllo di plausibilità sulle citazioni normative italiane ed europee prodotte da Claude (o passate dall'utente), senza nessuna superficie di rischio aggiuntiva.

## Cosa fa

`verifica-fonti` analizza un testo con riferimenti normativi italiani/UE — leggi, decreti, sentenze di Cassazione/Consiglio di Stato/TAR, regolamenti UE, provvedimenti del Garante Privacy, dell'AGCM, di Banca d'Italia — e ti dice se:

- il formato della citazione è coerente con lo standard di quel registro
- l'atto citato sembra esistere (tramite consultazione dei registri pubblici)
- non ci sono refusi categoriali (es. *art. 1382 c.c.* attribuito al "danno extracontrattuale" quando è la clausola penale)
- ci sono citazioni che non si riesce a risolvere e meritano un controllo umano

Invocazione tipica dopo una risposta di Claude con citazioni normative:

> *"Controlla le citazioni di questa risposta."*
> *"Passa l'output a verifica-fonti."*
> *"Queste citazioni reggono?"*

## Differenza con BeccarIA "piena" (`MicheleLoi/legal-tech-cowork`)

Il plugin BeccarIA completo include altre cinque skill (`catalogo`, `skill-installer`, `adattamento-italiano`, `ecosystem-scout`, `pattern-extractor`) che fanno fetch di un bollettino curato sul VPS `bulletins.micheleloi.pro` e propongono installazione di skill terze provenienti dall'ecosistema legal-AI open source.

Questo plugin (**solo controllo fonti**) **non fa nulla di tutto questo**:

- nessun fetch a un bollettino RegIA
- nessun catalogo di skill terze
- nessuna installazione automatica
- nessun pattern AGPL applicato dinamicamente

`verifica-fonti` fa `WebFetch` su pagine pubbliche dei registri italiani/UE (Normattiva, EUR-Lex, Garante Privacy, Corte Costituzionale, Cassazione) e — opzionalmente — usa l'estensione **Claude in Chrome** sul sito di Cassazione `italgiure.giustizia.it/sncass` se l'avvocato la installa. Se l'avvocato aggiunge **per propria scelta** un connettore MCP a una banca dati giuridica di terzi (es. BuddaLaw o Simpliciter), la skill può usarlo come prima ricerca — solo dopo consenso esplicito, con fallback automatico ai registri web — ma **nessun connettore è incluso o richiesto** da questo plugin: di default opera senza dipendenze esterne oltre ai registri pubblici.

**Scegli questo plugin se** vuoi un controllo coerenza fonti senza dipendere da un server di curazione gestito da terzi.

**Scegli BeccarIA piena** (`MicheleLoi/legal-tech-cowork`) se vuoi anche l'esperienza di esplorazione dell'ecosistema legal-AI open source italiano.

## Installazione

In Claude Code o Cowork:

```
/plugin marketplace add MicheleLoi/beccaria-solo-controllo-fonti
/plugin install beccaria-solo-controllo-fonti@beccaria-solo-controllo-fonti
```

### Allowlist egress

Per consentire alla skill di consultare i registri pubblici, in **Claude Desktop** aggiungi i seguenti domini all'allowlist `WebFetch`:

- `normattiva.it`
- `eur-lex.europa.eu`
- `gpdp.it` (Garante Privacy)
- `cortecostituzionale.it`
- `italgiure.giustizia.it`
- `agenziaentrate.gov.it`
- `consiglionazionaleforense.it`
- `agcm.it`
- `anticorruzione.it`
- `bancaditalia.it`

(Non è richiesto nessun dominio `micheleloi.pro` — questo plugin non chiama il VPS RegIA.)

### Cassazione via Chrome (opzionale, raccomandato)

Per verifiche più precise sulle pronunce di legittimità, installa l'estensione **Claude in Chrome** ([guida italiana di Avv. Giovanna Panucci](https://avvocatogiovannapanucci.substack.com/p/notizie-dallarena-n-120-claude-ora)) e autorizzala. La skill potrà allora aprire direttamente `italgiure.giustizia.it/sncass` ed eseguire la ricerca sul DB ufficiale di Cassazione invece di limitarsi alle pagine statiche pubbliche.

## Licenza

[AGPL-3.0-only](LICENSE) — copyleft di rete. Se modifichi e distribuisci (anche come servizio di rete), devi rendere disponibile il sorgente modificato sotto la stessa licenza.

## Autore

Michele Loi — parte del progetto [RegIA](https://micheleloi.pro/regia/) (azienda abilitatore per l'avvocato italiano nell'ecosistema open source legal-AI).

## Repo correlato

- [`MicheleLoi/legal-tech-cowork`](https://github.com/MicheleLoi/legal-tech-cowork) — BeccarIA completa (6 skill, bollettino RegIA, ecosystem-scout, pattern-extractor)
