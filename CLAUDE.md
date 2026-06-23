# X CROSS Training — Istruzioni per Claude Code

> 👉 **Ripresa sessione**: leggi [`STATO-PROGETTO.md`](STATO-PROGETTO.md) per stato attuale, come riprendere e prossimi passi.

## Cos'è questo progetto
App mobile per la **programmazione di allenamenti cross-training / functional**. L'utente (allenatore o atleta) imposta il proprio profilo e massimali, sceglie sistema di allenamento e modalità, e l'app genera **combinazioni di esercizi** (Pesistica / Ginnastica / Locomozione) su breve termine (un workout), medio termine (mesociclo) e lungo termine (stagione), con timer, parametri di carico, video e musica.

Ideatore: Graziano De Luca. Questo repository è un **handoff di specifiche**: contiene documentazione, modello dati e dataset. **Il codice Flutter non è ancora stato scritto** — è il prossimo passo.

## Stack target
- **Flutter** (Dart), mobile cross-platform iOS + Android.
- State management e package: vedi `docs/07-architettura-flutter.md` (proposta, non vincolante).

## Convenzioni
- **Tutta la documentazione e i commenti sono in italiano.**
- I codici esercizio (`P1`, `G3`, `L2`, …) sono identificativi stabili: non rinominarli.
- I dataset in `data/*.json` sono la **fonte di verità** per esercizi, modalità e tabelle: l'app li carica come asset.

## Da dove iniziare (ordine di lettura consigliato)
1. [`docs/00-visione-prodotto.md`](docs/00-visione-prodotto.md) — perché esiste, target, value proposition
2. [`docs/01-specifiche-funzionali.md`](docs/01-specifiche-funzionali.md) — elenco funzionalità
3. [`docs/02-modello-dati.md`](docs/02-modello-dati.md) — entità ed enum (fondamenta)
4. [`docs/03-algoritmo-combinazioni.md`](docs/03-algoritmo-combinazioni.md) — **CUORE TECNICO**: generatore combinazioni senza ripetizione
5. [`docs/04-modalita-allenamento.md`](docs/04-modalita-allenamento.md) — EMOM, Tabata, AMRAP, For Time, 300, EDT…
6. [`docs/05-schemi-reps-percentuali.md`](docs/05-schemi-reps-percentuali.md) — tabelle reps↔%1RM e metabolismi
7. [`docs/06-dieta-zona.md`](docs/06-dieta-zona.md) — modulo nutrizione (dieta a Zona)
8. [`docs/07-architettura-flutter.md`](docs/07-architettura-flutter.md) — architettura proposta
9. [`docs/08-roadmap-mvp.md`](docs/08-roadmap-mvp.md) — fasi di sviluppo e priorità
10. [`docs/09-guida-flutter-da-zero.md`](docs/09-guida-flutter-da-zero.md) — Flutter per chi non l'ha mai usato

## Design (fase conclusa)
Il design è stato prodotto e consegnato. In `design/` restano solo gli output utili allo sviluppo:
- [`design/03-template-linee-guida.md`](design/03-template-linee-guida.md) — **linee guida compilate**: 5 direzioni (A·Steel, B·Volt, C·Ember, D·Forge, E·Pulse) con palette HEX/Pantone, tipografia, forme, componenti. **Fonte di verità del tema Flutter** (già implementato in `app/lib/core/theme/`).
- [`design/mockup/X-Cross-Training-mockup.html`](design/mockup/X-Cross-Training-mockup.html) — prototipo interattivo autonomo (switch A–E, schermate S0–S13, timer Tabata) + screenshot `S0…S9.png` come riferimento visivo.

## Dataset
- [`data/esercizi.json`](data/esercizi.json) — libreria P1–P18 / G1–G18 / L1–L4
- [`data/modalita.json`](data/modalita.json) — parametri delle modalità
- [`data/reps-percentuali.json`](data/reps-percentuali.json) — tabella 1RM

## App Flutter (scaffold MVP)
La cartella [`app/`](app/README.md) contiene lo scaffold Flutter dell'MVP, costruito sulle linee guida di design:
- **Design system** in `app/lib/core/theme/` — token centralizzati e 5 temi selezionabili (A·Steel, B·Volt, C·Ember, D·Forge, E·Pulse) con toggle chiaro/scuro.
- **Componenti riutilizzabili** in `app/lib/widgets/`.
- **Schermate S0–S9** in `app/lib/features/` fedeli al mockup, con timer Tabata funzionante e generatore combinazioni in `app/lib/domain/`.
- Avvio: `cd app && flutter create . && flutter pub get && flutter run` (vedi `app/README.md` e `docs/09`).

## Materiale sorgente
In `sorgenti/` ci sono i file originali (PPT e Excel) e in `sorgenti/estratti/` la trascrizione testuale leggibile. L'Excel è il **prototipo dell'algoritmo combinazioni** descritto nel doc 03.
