# Pubblica il tuo primo libro #

**easybook** è un'applicazione che ti consente di creare facilmente un libro
in diversi formati elettonici. Inizialmente è stato concepito per la
realizzazione di libri tecnici relativi alla programmazione, ma potete usare
**easybook** per pubblicare novelle, manuali, libri tecnici e siti web con la
documentazione del vostro progetto.

Prima di iniziare ad usare **easybook** controllate di avere installato e
configurato PHP 5.3.2 o superiori sul vostro computer. Se non avete compreso
la frase precedente, chiedi consiglio ad un amico esperto di computer e
mandalo a questa pagina. Potete controllare la versione di PHP installata
lanciando il seguente comando nel terminale:

    [cli]
    php -v

**easybook** è un applicazione gratuita e open-source pubblicata sotto licenza
MIT. Questo significa che potete farci qualsiasi cosa. La sola condizione è
che manteniate il file `LICENSE.md` incluso nel codice sorgente. Questo dile
spiega la licenza di **easybook** e i suoi autori originali.

In ogni caso voi siete i soli proprietari dei libri pubblicati con **easybook*,
inclusi tutti i diritti d'autore e correlati appplicati nel vostro stato di
residenza. NOn siete obbligati a condiviere questi lavori in nessuna forma,
anche se ne otterrete un beneficio economico.

## Scaricare easybook ##

Prima di scaricare **easybook**, create una directory. Per esempio:

  * Su Windows: `C:\Users\javier\projects\easybook`
  * Su Mac OS X: `/Users/javier/projects/easybook`
  * Su Linux: `/home/javier/projects/easybook`

Se avete Git installato sul vostro computer, potete scaricare **easybook**
clonando il repository pubblico con i seguenti comandi (sostituite `<dir>` con
il percorso della cartella creata precedentemente):

    [cli]
    $ git clone http://github.com/javiereguiluz/easybook.git <dir>

Se non usate Git, potete scaricare **easybook** in un file compresso `.zip`.
Non è innovativo come usare Git, ma funziona bene. Scaricate il seguente file
e decomprimetelo nella cartella creata precedentemente:
<http://github.com/javiereguiluz/easybook/zipball/master>

### Usare easybook ###

Una volta scaricato/decompresso, aprite un terminale ed eseguite il seguente
script PHP per controllare di avere scaricato **easybook** correttamente:

    [cli]
    $ ./book

Se tutto è a posto, **easybook** vi darà il benvenuto con il seguente
messaggio:

    [cli]
                        |              |
    ,---.,---.,---.,   .|---.,---.,---.|__/
    |---',---|`---.|   ||   ||   ||   ||  \
    `---'`---^`---'`---|`---'`---'`---'`   `
                   `---'

    easybook is the easiest and fastest tool to generate
    technical documentation, books, manuals and websites.

    Available commands:
      help      Displays help for a command
      list      Lists commands
      new       Creates a new empty book
      publish   Publishes an edition of a book
      version   Shows installed easybook version

Se rilevate qualche problema nell'eseguire lo script `./book`, provate
eseguendolo come `php book`. Se continuate ad avere problemi controllate i
permessi dello script `book`. Se tutte le operazioni sopra indicate non
risolvono il problema, chiedete ancora al vostro amico esperto di computer.

Lo script `./book` è l'unico *punto di ingresso* per ogni comando di
**easybook**. Se vi serve saapere la versione installata, ad esempio, dovete
semplcemente eseguire il comando `version` attraverso lo script `book`:

    [cli]
    $ ./book version


                        |              |
    ,---.,---.,---.,   .|---.,---.,---.|__/
    |---',---|`---.|   ||   ||   ||   ||  \
    `---'`---^`---'`---|`---'`---'`---'`   `
                   `---'

    easybook installed version: 4.2

## Creare il libro ##

In questa sezione creerete il vostro primo libro di esempio con **easybook**.
In alternativa, se volete provare **easybook** il più velocemente possibile,
potete utilizzare i libri già pronti chiamati `easybook-doc-en` (la
documentazione in inglese di **easybook**) e `easybook-doc-es` (la
documentazione in spagnolo di **easybook**). In questo caso potete passare
alla sezione *Pubblicare il libro*.

**easybook** richiede che i vostri libri seguano una certa struttura delle
cartelle. Per creare questa struttura manualmente, i nuovi libri sono
inizializzati con il comando `new` di **easybook**:

    [cli]
    $ ./book new "L'origine delle specie"

Scrivendo il titolo del vostro libri dopo il comando `new` rachiuso tra
virgolette. Il risultato di questo comando è una nuova cartella
`l-origine-delle-specie` nella cartella `doc/` di **easybook**. Potete vedere
la seguente struttura dentro la cartella:

    <easybook>/
        doc/
            l-origine-delle-specie/
                config.yml
                Contents/
                    chapter1.md
                    chapter2.md
                    images/
                Output/

Queste sono i file e le cartelle create da **easybook**:

  * `config.yml`, questo file contiene tutte le opzioni di configurazione del
    libro. Analizzeremo queste opzioni nelle prossime sezioni e capitoli, ma
    probabilmente vorrete cambiare l'opzione `author` per impostare l'autore
    del libro (ad esempio, `Charles Darwin`).
  * `Contents/`, questa cartella contiene tutto il contenuti del libro (testo
    e immagini). **easybook** crea due capitoli di esempio (`chapter1.md` e
    `chapter2.md`) e una cartella `images/` vuota.
  * `Output/`, inizialmente questa cartella è vuota, ma conterrà il libro
    pubblicato.

## Scrivere il libro ##

I contenuti del libro sono scritti in file di testo usando la sintassi
Markdown. Questo formato è diventato lo standard *de facto* per la scrittura
di documentazione per Internet. Se non avete familiarità con la sintassi
Markdown, leggete le [specifiche ufficiali della sintassi Markdown](http://daringfireball.net/projects/markdown/syntax).
Markdown è l'unico formato attualmente supportato da **easybook**. In futuro
alcuni altri formati verranno supportati, quali reStructuredText, Textile ed
altri formati meno usati.

Ora, dimenticatevi **easybook** per un attimo, e scrivete i contenuti del
vosrto libro in Markdown usando il vostro editor di testo preferito (`vi`,
*Notepad*, *TextMate*, *SublimeText*, etc.).

La struttura di un libro piò essere veramente complessa (copertina, pagina con
titolo, dediche, capitoli, sezioni, ...). **easybook** supporta tutti i tipi
comuni di libro, ma per ora, ci focalizzeremo sui capitoli. Potete aggiungere
tutti i capitoli che desiderate ed ognuno può essere lungo o corto quanto
desiderate. Tutto quello che dovete fare è elencare tutti i capitoli
nell'opzione `contents` del file `config.yml`:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: chapter2.md }

Ogni linea successiva all'opzione `contents` definisce un contenuto del libro.
Le linee `cover` e `toc` sono contenuti speciali che spiegheremo
successivamente. Aggiungete i capitoli del vostro libro con elementi
`chapter`, indicate la loro numerazione (con l'opzione `number`) e il nome dei
file che li contengono (con l'opzione  `content`).

Oltre all'estrema leggerezza, la caratteristica principale di **easybook** è
la sua flessibilità, che non vi forzerà mai a lavorare in un certo modo.
Volete numerare i capitoli in una maniera *atipica*? Le persone penseranno che
siete dei pazzi, ma **easybook** vi consentirà di farlo;

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 100, content: chapter1.md }
            - { element: chapter, number: 56,  content: chapter2.md }

Volete utilizzare lettere al posto di numeri? Questoè abbastanza usuale per le
appendici e non per i capitoli, ma **easybook** non vi impiedirà di farlo:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: A, content: chapter1.md }
            - { element: chapter, number: B, content: chapter2.md }

Potete anche usare qualsiasi nome per i file che conterranno i capitoli, come
nell'esempio seguente che mischia inglese e spagnolo:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: capitulo2.md }

Usare nome significativi per i file dei contenuti del libro rendono più
falicle la loro gestione:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: publishing-your-first-book.md }
            - { element: chapter, number: 2, content: publishing-your-second-book.md }

La cosa più importante relativa all'opzione `content` è l'ordine in cui voi
definite i conenuti. Il libro pubblicato conterrà sempre i contenuti nello
stesso ordine. Ad esempio, la configurazione seguente, genererà un libro con
la copertina tra i primi due capitoli e l'indice alla fine (complemtamente
insensato, ma veramente semplice da fare con **easybook**):

    [yaml]
    book:
        # ...
        contents:
            - { element: chapter, number: 1, content: publishing-your-first-book.md }
            - { element: cover }
            - { element: chapter, number: 2, content: publishing-your-second-book.md }
            - { element: toc   }

Tutti i file dei contenuti sono archiviati, in maniera predefinita,
all'interno delle cartella `Contents/`.

Probabilmente, se il vostro libro ha una certa complessità, dividerete i
contenuti in sotto cartelle, quindi neell'opzione `content` dovrete includere
anche il nome delle sottocartelle (non dimenticatevi di racchiudere tra
virgolette il percorso se contiene degli spazi):

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: introduction/chapter1.md }
            - { element: chapter, number: 2, content: introduction/chapter2.md }
            - { element: chapter, number: 3, content: advanced/chapter1.md }

La configurazione qui sopra indica che i contenuti del vostro libro sono
distribuiti nella seguente maniera:

    <book_dir>/
        ...
        Contents/
            introduction/
                chapter1.md
                chapter2.md
            advanced/
                chapter1.md


## Pubblicare il libro ##

Quanto avete finito di scrivere tutti i capitoli e dopo averli aggiunti al
file `config.yml`, eseguite il seguente comando per pubblicare il libro
(sostituite `l-origine-delle-specie` con il nome della certella del vostro
libro):

    [cli]
    $ ./book publish l-origine-delle-specie web

Se tutto funziona correttamente, potrete cedere una nuova cartella `web`
dentro la cartella `Output/` e potrete trovarvi all'interno un file nominato
`book.html`. Questo è il libro completo nel formato HTML, pronto per essere
pubblicato in Internet.

In seguito eseguite il seguente comando:

    [cli]
    $ ./book publish l-origine-delle-specie website

Ora, dentro la cartella `Output/` potete trovare una nuova cartella `website`
con diversi file HTML. Aprite `index.html` nel vostro browser e potete vedere
che **easybook** ha pubblicato il vostro libro come un sito statico
completamente funzionante.

Eseguite il seguente comando per generare un e-book:

    [cli]
    $ ./book publish l-origine-delle-specie ebook

Nella cartella `Output/` del vostro libro potete trovare una nuova cartella
`ebook` con un file nominato `ebook.epub`. Questa è la versione e-book del
vostro libro, pronto per essere letto da qualsiasi dispositivo `.ePub`
compatibile (tablet iPad, telefono iPhone, la maggior parte dei tablet e
telefoni Android e ogni lettore di e-book eccetto Amazion Kindle).

Infine, lanciate il seguente comando:

    [cli]
    $ ./book publish l-origine-delle-specie print

Nella cartella `Output/` potrete trovare una nuova cartella `print` che
contiene un file chiamato `book.pdf`. Aprite il nuovo file con il vostro
lettore di PDF  e potrete vedere il vostro libro velocemente trasformato in un
PDF piacevolmente impaginato. La conversione in PDF è realizzata attraverso un
applicazione esterna chiamata [PrinceXML](http://www.princexml.com/).

Se non lo avete installato all'interno del vostro computer, potete scaricarne
una versione completamente funzionante nella versione dimostrativa alla pagina
<http://www.princexml.com/download/>

**easybook**vi da la possibilità di pubblicare facilmente lo stesso libro in
diversi modi. Ognuna di queste *modalità* è chiamata **edizione**. Questo
concetto verrà appproondito nel prossimo capitolo.


## Opzioni di configurazione del libro ##

Nella sezione precedente abbiamo menzionato l'opzione di configurazione `author`. In effetti, ééeasybook** ouò impostare molte opzioni per i libri all'interno del file `config.yml`. I valori predefiniti delle opzioni sono le seguenti:

    [yaml]
    book:
        title:            "(il nome inserito nella creazione del libro)"
        author:           "Change this: Author Name"
        edition:          "First edition"
        language:         en
        publication_date: ~

        generator: { name: easybook, version: 4.2 }

        contents:
            # available content types: acknowledgement, afterword, appendix, author,
            # chapter, conclusion, cover, dedication, edition, epilogue, foreword,
            # glossary, introduction, license, lof (list of figures), lot (list of
            # tables), part, preface, prologue, title, toc (table of contents)
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: chapter2.md }

        editions:
            ebook:
                # (this is a complex option, we'll see it later)
            print:
                # (this is a complex option, we'll see it later)
            web:
                # (this is a complex option, we'll see it later)
            website:
                # (this is a complex option, we'll see it later)

Le opzioni `contents` ed `editions` sono spiegati nel dettaglio nei capitoli
seguenti: l'opzione `contents` definisce il contenuti del libro ed il loro
ordine; l'opzione `editions` definisce le caratteristiche per ogni edizione
del libro.

Le altre opzioni impostano alcune in formazioni di base del libro:

  * `title`, è il titolo del libro. In maniera predefinita **easybook**
  utilizza il titolo che avete inserito in fase di creazione del libro, ma
  potete modificarlo se lo ritenete opportuno.
  * `author`, è il nome dell'atore del libro. Se il libo ha più autori,
  inseritli separati da una virgola:
  `"Nome1 Cognome1, Nome1 Cognome2, ..."`
  * `edition`, è il testo che descrive l'edizione del libro. Normalmente
  inserirete *prima edizione*, *seconda edizione* e così via, ma potete
  descrivere l'edizione del lvostro libro anche in qualsiasi altro modo.
  * `language`, la lingua del contenuto del libro nel formato a due caratteri:
  `en` per l'inglese, `es` per lo spagnolo, `fr` per il francese, `it`per
  l'italiano, `de` per il tedesco, etc.
  * `publication_date`, la data di pubblicazione del libro. Il valore
  predefinito è `~`, che indica nessuna data di pubblicazione. In questo caso
  **easybook** imposterà la data in maniera automatica alla data in cui il
  libro è stato pubblicato. Se impostate la data, inseritela nelformato
  `mese-anno-giorno`. ad esempio:
  `11-23-2012`.
