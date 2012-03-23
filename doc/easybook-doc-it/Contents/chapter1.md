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

## Writing the book ##

Book contents are written in regular text archives using Markdown syntax.
This format has become the *de facto* standard for writing documentation for
Internet. If you are not familiar with Markdown syntax, read the [official
Markdown syntax reference](http://daringfireball.net/projects/markdown/syntax)
. Markdown is the only format currently supported by **easybook**. In the
future, many more formats will be supported, such as reStructuredText,
Textile and other widely used formats.

Therefore, forget **easybook** for a while and write the contents of your
book in Markdown syntax using your favorite text editor (`vi`, *Notepad*,
*TextMate*, *SublimeText*, etc.)

The structure of a book can be very complex (cover, title page,
acknowledgements, dedication, chapters, parts, etc.). **easybook** supports
all the common book content types, but for now, we'll just focus on the
chapters. You can add as many chapters as you want and each one can be as
large or as short as you need. All you have to do is to list the book
chapters under the `contents` option of the `config.yml` file:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: chapter2.md }

Each line under the `contents` option defines a content of the book. The
`cover` and `toc` lines are special contents that will be explained later.
Add your book chapters as  `chapter` elements and set their number (with the
`number` option) and the name of the files that hold their contents (with the
`content` option).

Besides being lightning-fast, the main feature of **easybook** is its
flexibility, as it never forces you to work in a certain way. Do you want to
number your chapters in an *imaginative* way? People will think you're crazy,
but **easybook** allows you to do it:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 100, content: chapter1.md }
            - { element: chapter, number: 56,  content: chapter2.md }

Do you need letters instead of numbers? This is usual for appendices instead
of chapters, but **easybook** won't stop you from doing it:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: A, content: chapter1.md }
            - { element: chapter, number: B, content: chapter2.md }

You can also use any name for the chapter contents file, as in the following
example that mixes English and Spanish:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: capitulo2.md }

Using significant names for book content files eases its management:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: publishing-your-first-book.md }
            - { element: chapter, number: 2, content: publishing-your-second-book.md }

The most important thing about the `contents` option is the order in which
you define the contents. The published book will be always composed of those
contents and in that order. Therefore, the following configuration will
output a book with  the cover between the two chapters and the table of
contents at the very end (completely crazy, but really easy to do with
**easybook**):

    [yaml]
    book:
        # ...
        contents:
            - { element: chapter, number: 1, content: publishing-your-first-book.md }
            - { element: cover }
            - { element: chapter, number: 2, content: publishing-your-second-book.md }
            - { element: toc   }

By default, all content files are stored in the `Contents/` directory.
However, if your book is complex, you can divide the contents into
subdirectories. Then, include the name of the subdirectories in the `content`
option  (don't forget to enclose it with quotes if the file path has spaces):

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: introduction/chapter1.md }
            - { element: chapter, number: 2, content: introduction/chapter2.md }
            - { element: chapter, number: 3, content: advanced/chapter1.md }

The above configuration means that your book contents are distributed this
way:

    <book_dir>/
        ...
        Contents/
            introduction/
                chapter1.md
                chapter2.md
            advanced/
                chapter1.md


## Publishing the book ##

When you finish writing all the chapters and after adding them to the
`config.yml` archive, run the following command to publish the book (replace
`the-origin-of-the-species` by the name of your book directory):

    [cli]
    $ ./book publish the-origin-of-species web

If everything works fine, you should see a new `web` directory inside
`Output/` directory. Enter the `web/` directory and you'll find a file named
`book.html`. This is the complete book in HTML format, ready to publish it on
the Internet.

Then, run the following command:

    [cli]
    $ ./book publish the-origin-of-species website

Now, inside `Output/` directory you'll find a new `website` directory with
several HTML pages. Open `index.html` in your browser and you'll see that
**easybook** has published your book as a fully-functional static website.

Run the following command to generate an e-book:

    [cli]
    $ ./book publish the-origin-of-species ebook

Inside your book's `Output/` directory you'll find a new `ebook` directory
with a file named `book.epub`. This is the e-book version of your book, ready
to be read in any `.ePub` compatible reader (iPad tablets, iPhone phones,
most Android tablets and phones and every e-book reader except Amazon Kindle).

Lastly, run the following command:

    [cli]
    $ ./book publish the-origin-of-species print

Inside `Output/` directory you'll find a new `print` directory which contains
a file name `book.pdf`. Open the file with your PDF reader and you'll see
your book as a beautiful and carefully created PDF ebook. The PDF conversion
is made with an external application named [PrinceXML](http://www.princexml.com/).
If you don't have it installed on your computer, you can download a
fully-functional demo version at <http://www.princexml.com/download/>

**easybook** lets you easily publish the same book in very different ways.
Each of these *ways*  is called **edition**. This concept will be explained
in the next chapter.

## Book configuration options ##

In the previous sections we've mentioned the `author` configuration option.
In fact, **easybook** books can set many more options in the `config.yml` file
. The default values of the options are as follows:

    [yaml]
    book:
        title:            "(the title typed when creating the book)"
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

The `contents` and `editions` options are explained in  detail in the
following chapters: `contents` option defines the book contents and their
order; `editions` option defines the features of each edition of the book.

The other options set the basic information of the book:

  * `title`, is the title of the book. By default **easybook** uses the title
  that you typed when creating the book, but you can change it if needed.
  * `author`, is the name of the book author. If the book has multiple
  authors, write them all in a row separated by commas:
  `"Name1 Surname1, Name2 Surname2, ..."`
  * `edition`, is the text describing the edition of the book. Normally, you
  should use *first edition*, *second edition* and so on, but you can
  describe your book current edition in any way.
  * `language`, the language of the book contents set with a two letter code:
  `en` for English, `es` for Spanish, `fr` for French, `it` for Italian, `de`
  for Deutsch, etc.
  * `publication_date`,  the date of publication of the book. The default
  value is `~`, meaning no publication date. In this case, **easybook** will
  automatically set the date to the day on which the book is published. If
  you set a date, enter it in the `month-day-year` format. For example:
  `11-23-2012`.

