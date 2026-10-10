# BASILICO-BB-C64

**BASato sull'Italiano LInguaggio COnvertito, derivato dal BBC BASIC per Commodore 64**

BASILICO-BB-C64 è un adattamento del celebre linguaggio **BBC BASIC** per Commodore 64, caratterizzato dalla localizzazione dei comandi in lingua italiana. Allo stato attuale, le parole chiave e le istruzioni del BASIC sono state interamente tradotte, mentre i messaggi di errore rimangono in fase di completamento.

---

## Compatibilità e Interscambiabilità dei Sorgenti

Grazie alla struttura interna ereditata dal BBC BASIC, le istruzioni del linguaggio non vengono salvate come testo in chiaro, ma sotto forma di **token numerici**. Questo garantisce la piena compatibilità bidirezionale tra i programmi:

- **Da BBC BASIC a BASILICO**: Un programma salvato in BBC BASIC (nella versione C64 sviluppata da J.G. Harston) può essere caricato in BASILICO. Le parole chiave verranno automaticamente mostrate e interpretate con i corrispettivi comandi in italiano.
- **Da BASILICO a BBC BASIC**: Un programma salvato in BASILICO, una volta riaperto nell'ambiente BBC BASIC originale, mostrerà ed eseguirà i comandi nella loro forma inglese standard.

### Note e Avvertenze sulle Variabili
Sebbene la struttura del codice rimanga perfettamente compatibile, occorre prestare attenzione ai **nomi delle variabili**:
1. Poiché BASILICO utilizza parole chiave in italiano, un nome di variabile valido in BBC BASIC inglese potrebbe coincidere con una nuova istruzione riservata in BASILICO (e viceversa), generando conflitti di sintassi.
2. È sempre consigliabile scegliere nomi di variabili neutri o verificare che non coincidano con le parole chiave tokenizzate della versione di destinazione.

---

## Requisiti e Utilizzo

Per eseguire **BASILICO-BB-C64** su un emulatore Commodore 64 (es. VICE, anche in versione browser/online) o su un reale Commodore 64 / 128:

1. Scaricare il file PRG del sistema.
2. Caricarlo ed eseguirlo tramite il comando:
```basic
LOAD "BASILICO-BB",8
RUN
```

---

## Utility DISCO e Gestione dei File

Il linguaggio originale non dispone di comandi nativi per le operazioni di I/O su disco (come la lettura della directory, la rinomina dei file, l'inizializzazione o la formattazione di un floppy). Per colmare questa mancanza, all'interno del repository è inclusa l'utility **DISCO**, che integra tutte le funzionalità di gestione dei file necessarie.

---

## Assemblatore Integrato

L'utility DISCO è interamente sviluppata in Assembly sfruttando l'**assemblatore integrato** ereditato dal BBC BASIC. Durante la programmazione in Assembly all'interno dell'ambiente BASILICO, occorre tenere presenti alcune particolarità sintattiche e di architettura:

* **Mnemonico ORA**: L'istruzione `ORA` (Logical OR with Accumulator) è espressa dal mnemonico **`OA`**.
* **Notazione Esadecimale**: Il prefisso per i valori esadecimali è **`&`** (anziché il classico simbolo `$` comunemente impiegato negli assemblatori per C64).
* **Accesso ai Registri Video/IO (`&D020` / `&D021`)**: Per modificare direttamente i colori di bordo e sfondo tramite le locazioni di memoria `&D020` e `&D021`, è indispensabile commutare preventivamente la configurazione di memoria del registro CPU `&01` per rendere visibili i registri I/O al posto della ROM. Il blocco di codice deve essere strutturato come segue:

```assembly
SEI          ; Disabilita gli interrupt
LDA &01
PHA          ; Salva la configurazione di memoria corrente sullo stack
LDA #&36     ; Seleziona la mappa di memoria con I/O abilitato
STA &01

; --- Inizio codice di modifica registri I/O (es. &D020 / &D021) ---
; ...
; --- Fine codice di modifica ---

PLA          ; Ripristina la configurazione di memoria originale
STA &01
CLI          ; Riabilita gli interrupt
```

---

## Proprietà Intellettuale e Note sui Diritti

Questo progetto è una modifica di un'opera preesistente e non rivendica la titolarità del codice sorgente o del binario originale. La proprietà intellettuale è così suddivisa:

- **BBC BASIC (Core & Implementazione 6502)**: Tutti i diritti relativi al codice originale appartengono a **Acorn Computers Ltd.** (e ai suoi aventi causa).
- **Interfaccia per Commodore 64**: Il porting e l'adattamento tra l'architettura BBC BASIC e il KERNAL Commodore 64 sono stati sviluppati da **J.G. Harston** ([mdfs.net](http://mdfs.net/Software/BBCBasic/C64/)).
- **Localizzazione in Italiano**: La traduzione dei token, l'adattamento della sintassi italiana e la conseguente riallocazione dei byte sono a cura dell'autore di questo repository.

Il codice sorgente originale e i file derivati rimangono soggetti alle rispettive note di copyright dei detentori dei diritti (**Acorn Computers** e **J.G. Harston**).

---

## Crediti

Un ringraziamento speciale a **J.G. Harston** per il prezioso lavoro di porting del BBC BASIC sul Commodore 64 e a **Sophie Wilson** unitamente a **Acorn Computers** per la creazione del linguaggio originale.