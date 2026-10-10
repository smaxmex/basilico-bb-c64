# BASILICO-BB-C64

**BASato sull'Italiano LInguaggio COnvertito, derivato dal BBC BASIC per Commodore 64**

BASILICO-BB-C64 è un adattamento del linguaggio BBC BASIC per Commodore 64 con comandi localizzati in lingua italiana. Allo stato attuale, i comandi del BASIC sono stati interamente tradotti, non ancora i messaggi di errore.

---

## Proprietà intellettuale e note sui diritti relativi al codice

Questo progetto rappresenta una modifica di un'opera preesistente e non rivendica la titolarità del codice sorgente o del binario originale. La proprietà intellettuale delle componenti del software è articolata come segue:

- **BBC BASIC (Core & Implementazione 6502)** - Tutti i diritti relativi al codice originale del BBC BASIC appartengono a **Acorn Computers Ltd.** (e ai suoi aventi causa).
- **Interfaccia per Commodore 64** - Il codice di adattamento e interfacciamento tra il BBC BASIC e il Kernal del Commodore 64 è stato sviluppato da **J.G. Harston** ([mdfs.net](http://mdfs.net/Software/BBCBasic/C64/)).
- **Localizzazione dei Comandi in Italiano** - La paternità della traduzione, dell'adattamento dei token e della riallocazione dei byte relativi alla sintassi in lingua italiana appartiene all'autore di questo repository.

Il codice originale del BBC BASIC e l'adattamento per Commodore 64 rimangono soggetti alle rispettive note di diritto d'autore originali dei detentori dei diritti (**Acorn Computers** e **J.G. Harston**).

---

## Requisiti e Utilizzo

Per eseguire **BASILICO-BB-C64** su un emulatore Commodore 64 (es. VICE) o su reale Commodore 64/128:

1. Scaricare il file PRG.
2. Caricarlo tramite comando:
```basic
LOAD "BASILICO-BB",8
RUN
```

---

## Utility DISCO per la gestione dei file

Poiché BASILICO non dispone di comandi nativi per la gestione dei file (come la visualizzazione della directory, la rinomina dei file, l'inizializzazione o la formattazione del disco), è stata inserita nel repository l'utility **DISCO**, che integra queste funzionalità.

## L'assemblatore integrato

L'utility DISCO è scritta in Assembly attraverso l'assemblatore integrato che BASILICO eredita dal BBC BASIC, ed è perfettamente funzionante. Durante la programmazione, occorre tenere presenti alcune particolarità della sintassi dell'assemblatore integrato:

- Il mnemonico `ORA` in BASILICO è **`OA`**.
- In BASILICO il prefisso per i numeri esadecimali è **`&`** (anziché il classico `$` utilizzato solitamente dagli assemblatori per Commodore 64).
- Non si possono modificare direttamente le locazioni di memoria `&D020` e `&D021` per cambiare i colori di bordo e sfondo se prima non si disattiva/sostituisce il banco ROM/IO tramite il registro di controllo CPU (`&01`). Per fare ciò, occorre racchiudere le modifiche tra le seguenti istruzioni:

```assembly
SEI
LDA &01
PHA
LDA #&36
...
; Codice di modifica registri I/O (es. &D020 / &D021)
...
PLA
STA &01
CLI
```

---

## Crediti

Un ringraziamento speciale a **J.G. Harston** per il lavoro di porting del BBC BASIC sull'architettura Commodore 64 e a **Sophie Wilson** e **Acorn Computers** per la creazione del linguaggio originale.
