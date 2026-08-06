# X CROSS Training

X CROSS Training e' un'app mobile Flutter per programmare allenamenti di cross-training e functional training, costruita a partire da un set di specifiche e dataset ricavati da una presentazione PowerPoint e da un foglio di calcolo Excel gia' esistenti. Il repository e' nato come pacchetto di sole specifiche (documenti, modello dati, dataset JSON) da consegnare a uno sviluppatore, ed e' poi cresciuto fino a includere uno scaffold Flutter vero e proprio: design system, componenti riutilizzabili e le schermate principali dell'app.

## Cuore tecnico: il generatore di combinazioni

L'idea centrale del prodotto e' costruire gli allenamenti combinando esercizi provenienti da tre famiglie, pesistica, ginnastica e locomozione, in combinazioni senza ripetizioni di uno, due o tre elementi lungo un ciclo di allenamento. La progettazione (documentata in `docs/03-algoritmo-combinazioni.md`) deriva da un prototipo Excel funzionante che usava `RANDBETWEEN` su un intervallo decrescente per estrarre combinazioni senza reinserimento, una variante dell'algoritmo di Fisher-Yates. Nel codice Flutter questa logica e' implementata in `app/lib/domain/combination_generator.dart` come classe `CombinationGenerator`, con filtri per attrezzatura disponibile, livello dell'atleta e gruppi di esercizi abilitati, ed e' logica pura senza dipendenze da Flutter, quindi testabile in isolamento (`app/test/combination_generator_test.dart`).

## Stato di sviluppo

Il repository contiene oggi piu' di una semplice pianificazione: sotto `app/` esiste uno scaffold Flutter con un design system a token centralizzati e cinque temi selezionabili, componenti riutilizzabili, le schermate S0-S9 fedeli al mockup di design, un timer Tabata funzionante e il generatore di combinazioni con i suoi test. Questo scaffold pero' non e' mai stato compilato ne' eseguito: Flutter non e' installato sulla macchina di sviluppo su cui e' stato scritto, quindi il codice e' stato scritto e revisionato staticamente ma non verificato con una build reale. I dati usati dall'app (`assets/data/*.json`) sono copie dei dataset in `data/`, ricavati a loro volta dai documenti originali in `sorgenti/` (il `.ppt` e il `.xlsm` di partenza, con relative estrazioni testuali). La modalita' Zona per la dieta (`docs/06-dieta-zona.md`) resta priva del dataset alimenti necessario, e non e' ancora stata cablata nell'app.

## Struttura del repository

```
app-cross-training/
├── docs/     specifiche funzionali, modello dati, algoritmo core, modalita' di allenamento,
│             architettura Flutter, roadmap MVP (00 -> 09, ordine di lettura consigliato)
├── data/     dataset JSON di riferimento: esercizi, modalita', tabella reps/percentuali 1RM
├── sorgenti/ file originali (.ppt, .xlsm) e le relative estrazioni testuali
└── app/      scaffold Flutter: design system, componenti, schermate S0-S9, generatore
              di combinazioni e relativi test
```

## Prossimi passi

La roadmap in `docs/08-roadmap-mvp.md` indica i passi successivi: verificare la compilazione dell'app in un ambiente con Flutter installato e risolvere gli eventuali errori segnalati da `flutter doctor`, scegliere una direzione grafica definitiva tra le cinque proposte e rimuovere il selettore tema, sostituire i dati di esempio con quelli reali in `assets/data/*.json`, e collegare il generatore di combinazioni al flusso di creazione del programma di allenamento.
