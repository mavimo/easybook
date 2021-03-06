# Pubblicare il vostro secondo libro #

Nel capitolo precedente avete imparato a creare e pubblicare un libro in
maniera basilare usando **easybook**. Finora non abbiamo menzionato nessuna
delle funzionalità avanzate. Questo capitolo spiegherà tutti i tipi di
contenuto disponibili, come gestire le edizioni del libro e come modificarne
la visualizzazione usando dei template.

## Tipi di contenuto ##

I libri definiscono il loro contenuto con l'opzione `contents` nel file
`config.yml`. Dopo aver creato un nuov libro con il comando `new`, il
contenuto predefinito è:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: toc   }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: chapter2.md }

L'opzione più importante di ogni contenuto è `element`, che definisce il suo
tipo di contenuto. **easybook** attualmente supporta 21 tipi di contenuto (le
sequenti definzioni sono [tratte da Wikipedia](http://en.wikipedia.org/wiki/Book_design)):

  * `acknowledgement`, spesso parte della prefazione, piuttosto che una parte
  a se stante. Riconosce coloro che hanno contribuito alla creazione del libro.
  * `afterword`, una parte di testo che descrive un intervallo di tempo
  successivo al tempo principale in cui si svolge la storia del libro.
  * `appendix`, è un aggiunta al contenuto principale del lavoro. Può
  contenere corresioni, spiegazioni di inconsistenze, dettagli o aggiornamenti
  delle informazioni che si trovano nel contenuto principale del libro.
  * `author`, informazioni sull'autore/autori del libro.
  * `chapter`, il ptipo più usato nei libri comuni.
  * `conclusion`, la fine del libro o documento, dove tutti i punti non
  chiari ci vengono presentati e chiariti o dove la tesi viene esposta.
  * `cover`, la copertina del libro.
  * `dedication`, una pagina che solitamente prcede il testo, in cui l'autore
  ringrazia le persone che l'hanno aiutato a realizzare il libro.
  * `edition`, informazioni relative all'edizione corrente del libro,
  comprensive della data di pubblicaizione.
  * `epilogue`, una parte del testo al termine del brano o dramma,
  abitualmente utilizzato per concludere il lavoro.
  * `foreword`, solitamente scritta da una persona differente dall'autore del
  libro. Si racconta spesso di una certa interazione tra l'autore della
  prefazione ed il contenuto del testo o tra lo scrittore e la storia.
  * `glossary`, consiste in una serie di definizioni di parole importanti per
  il contenuto del libro, solitamente in ordine alfabetico.
  * `introduction`, una sezione introduttiva in cui si presentano i propositi
  del testo a seguire.
  * `license`, informazioni sui diritti d'autore dell'autore o di altri
  autori/editori a cui il libro si attiene.
  * `lof` (*elenco delle figure*), è una lista ordinata delle immagini ed
  illustrazioni usate nel libro, comprensiva di numero e didascalia
  dell'immagine. La pagina in cui l'immagine si trova è presentata
  nell'edizione in `pdf`.
  * `lot` (*elenco delle tabelle*), una lista ordinata delle tabelle inserite
  all'interno del libro, comprensive del numero e disascalia. La pagina in cui
  la tabella si trova è inclusa per le edizioni in `pdf`.
  * `part`, utilizzata per raggruppare alcuni capitoli o appendici.
  * `preface`, generalmente spiega come la storia narrata nel libro è iniziata
  o l'idea dietro cuiè stato sviluppato il libro.
  * `prologue`, *scritto* dal narratore o da un qualsiasi altro personaggio
  del libro.
  E' un'apertura della storia che stabilisce il contesto in cui ci si trova ed
  alcuni dettagli, spesso qualche storia al contorno che si lega con quella
  principale.
  * `title`, la pagina iniziale che presenta il titolo e l'autore, solitamente
  assieme alle informazioni di pubblicazione del libro.
  * `toc` (*indice dei contenuti*), una lista delle parti del libro o
  documento disposte enell'ordine in cui queste appaiono.

La maggior parte dei tipi di contenuto non richiedono altre informazioni oltre
`element`:

    [yaml]
    book:
        # ...
        contents:
            - { element: cover }
            - { element: title }
            - { element: license }
            - { element: toc }
            - { element: chapter, number: 1, content: chapter1.md }
            - { element: chapter, number: 2, content: chapter2.md }
            - ...
            - { element: author }
            - { element: acknowledgement }

I tipi di contenuto `appendix` e `chapter` possono definire le seguenti
opzioni:

  * `number`, il numero del capitolo o appendice. Questo numero è utilizzato
  per generare le numerazioni delle diverse sezioni (`1.1`, `1.2`, `1.2.1`,
  `1.2.2`, etc.) **easybook** non si limita a questo formato, potete
  utilizzare numeri romani (`I.1`, `I.2`), lettere (`A.1`, `A.2`) o qulsiasi
  altro simbolo o stringa.
  * `content`, il nome del file che contiene questo elemento. Il file deve
  contenere l'estensione (`.md` nel caso di Markdown). Il valore di
  quest'opzione è interpretato come percorso dalla cartella`Contents/` del
  libro, quindi potete avere un numero qualsiasi di sottocartelle.

Il tipo di contenuto `part` definisce la seguente opzione:

  * `title`, il titolo della parte o sezione. In un libro stampato, una
  sezione è visualizzata come una pagina che spara dei capitoli. In un libro
  web, la sezione è mostrata come una testata.

Questi 21 tipi di contenuto definiti in **easybook** sono sufficienti a
pubblicare la maggiorparte dei libri, ma se lo ritente necessario, il prossimo
capitolo spiegherà come creare un nuovo tipo di contenuto.

## Edizioni ##

**easybook** è suuficientemente flessibile da consentire di pubblicare lo
stesso libro in differenti modalità. Questè p possibile grazie alle
**edizioni**, che definiscono le caratteristiche in cui il libro è pubblicato.

Le edizioni sono definite sotto l'opzione `editions` nel file `config.yml`. In
maniera predefinita, i libri creati con il comando `new`, hanno quttro
edizioni nominate `ebook`, `print`, `web` e `website` con le seguenti opzioni:

    [yaml]
    book:
        # ...
        editions:
            ebook:
                format:         epub
                highlight_code: false
                include_styles: true
                labels:         ['appendix', 'chapter']  # sono sisponibili anche le etichette: "figure", "table"
                toc:
                    deep:       1
                    elements:   ["appendix", "chapter", "part"]

            print:
                format:         pdf
                include_styles: true
                isbn:           ~
                labels:         ['appendix', 'chapter']  # sono sisponibili anche le etichette: 'figure', 'table'
                margin:
                    top:        25mm
                    bottom:     25mm
                    inner:      30mm
                    outter:     20mm
                page_size:      A4
                toc:
                    deep:       2
                    elements:   ["appendix", "chapter"]
                two_sided:      true

            web:
                format:         html
                highlight_code: true
                include_styles: true
                labels:         ['appendix', 'chapter']  # sono sisponibili anche le etichette: 'figure', 'table'
                toc:
                    deep:       2
                    elements:   ["appendix", "chapter"]

            website:
                extends:        web
                format:         html_chunked

Il nome di ogni edizioni deve essere unico per lo stesso libro e non possono
contenere spazi. I nomi delle edizioni sono usati come sottocartelle nella
cartella `Output/` per separare i contenuti di ogni edizione. Potete definire
tante edizioni quante ne ritenete necessarie, ma tutte devono appartenere a
uno dei seguenti quattro tipi definiti nell'opzione `format`:

  * `epub`, il libro verrà pubblicato come e-book chiamato `book.epub`
  * `pdf`, il libro verrà pubblicato come PDF chiamato `book.pdf`
  * `html`, il libro verrà pubblicato come pagina HTML chiamata `book.html`
  * `html_chunked`, il libro verrà pubblicato come un sito statico nella
  cartella chiamata `book`

Le edizioni possono modificare l'aspetto del libro pubblicato attraverso
diverse opzioni di configurazione. Le edizioni `epub`, `html` e `html_chunked`
condividono le stesse opzioni:

  * `highligh_code`, se `true` la sintassi del codice sarà evidenziata (questa
  opzione è momentaneamente non funzionante).
  * `include_styles`, se `true` gli stili CSS predefiniti di **easybook**
  saranno applicati.
  * `labels`, indica che i tipi di contenuto per cui **easybook** dovrà
  aggiungere l'etichetta all'inizio. In maniera predefinita le etichette sono
  aggiunte solo all'inizio dei capitoli e appendici. In aggiunta ai tipi di
  contenuto di **easybook** potete usare due valori speciali denominati
  `figure` e `table` per aggiungere le etichette alle immagini e alle tabelle
  del libro. Se non volete mostrare etichette nel vostro libro, cancellate
  tutti ii valori per questa opzione: `labels: []`.
  * `toc`, imposta le opzioni per l'indice degli contenuti. Verrà ignorato a
  meno che il libro contenga un elemento di tipo `toc`. HA due tipi di opzioni:
    * `deep`, il massimo livello di profondità che deve essere incluso
    nell'indice dei contenuti (`1` è il valore più piccolo consentito e
    mostrerà solo il livello `<h1>`; `6` è il valore più alto consentito e
    mostrerà i valori `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` e `<h6>`).
    * `elements`, il tipo di elementi inclusi nell'indie dei contenuti (in
    maniera predefinita solo `appendix`, `chapter` e `part` saranno inclusi).

Le edizioni `pdf` possono definire alcune opzioni aggiuntive:

  * `isbn`, il codice ISBN-10 o ISBN-13 del libro (questa opzione non è
  funzionante al momento).
  * `include_styles`, se `true` **easybook** definirà la struttura della
  pagina, le impoztaioni dei caratteri e l'aspetto grafico del libro. Usare
  quest'opzione per creare libri graficamente ben strutturati con basso sforzo.
  Il prossimo capitolo spiegherà come definire dei propri stili.
  * `labels`, è la stessa opzione che abbiamo visto per le edizioni `epub`,
  `html` e `html_chunked`.
  * `margin`, imposta i quattro margini del libro stampato: `top`, `bottom`,
  `inner` and `outter`. Se il libro ha pagine su un solo lato, `inner`
  corrisponde al margine sinistro e `outter` al margine destro. Il valore dei
  margini può essere impostato con ogni unità di misura vlide nei CSS (`1in`,
  `25mm`, `2.5cm`).
  * `page_size`, la dimensione della pagina del libro stampato. **easybook**
  supporta [decine di foramti pagina](http://www.princexml.com/doc/7.1/page-size/)
  grazie a PrinceXML: `US-Letter`, `US-Legal`, `crown-quarto`, `A4`, `A3`, etc.
  * `toc`,  è la stessa opzione che abbiamo visto per le edizioni `epub`,
  `html` e `html_chunked`.
  * `two_sided`, se `true` il file PDF sarà preparato per essere stamapato su
  due pagine affiancate.

In aggiunta a tutte queste opzioni, le edizioni possono avere un opzione
estremamente utile chiamata `extends`. Il valore di questa pzionie indica il
nome dell'edizione da qui l'edizione corrente *eredita*. Quando un edizione
*eredita* da un altra, le opzioni dell'edizione padre sono copiate
nell'edizione *corrente*, da cui ppoi possono essere sovrascritte.

Immaginaiamo, per esempio, che vogliamo pubblicare un PDF con tre formati
grafici differenti. La versione di bozza (`draft`) deve essere stampata su due
pagine e deve avere dei margini molto piccoli per ridurne la lunghezza, la
versione normale (`print`) è su una sola pagina ee ha dei margini normali. La
versione preparata per lulu.com (`lulu`) è simile alla versione normale,
tranne che è stampata fronte-retro:

    [yaml]
    book:
        # ...
        editions:
            print:
                format:       pdf
                isbn:         ~
                labels:       ['appendix', 'chapter']  # etichette disponibili anche per: 'figure', 'table'
                margin:
                    top:      25mm
                    bottom:   25mm
                    inner:    30mm
                    outter:   20mm
                page_size:    A4
                toc:
                    deep:     2
                    elements: ['appendix', 'chapter']
                two_sided:    false

            draft:
                extends:      print
                margin:
                    top:      15mm
                    bottom:   15mm
                    inner:    20mm
                    outter:   10mm
                two_sided:    true

            lulu:
                extends:      print
                two_sided:    true

La sola limitazione di `extends` è che funziona con un unico livello di
ereditarietà, pertanto un edizione non può estendere un altra edizione che ne
estende una terza.

## Temi ##

Un tema è un insieme di strutture, fogli di stile e altre risorse atte a
definire l'aspetto grafico dei libri. **easybook** include già un tema per
ogni tipo di edizione (`epub`, `pdf`, `html`, `html_chunked`), quindi i vostri
libri saranno presentati in maniera professionale anche senza nessuno sforzo.

I temi sono posizionati nella certalla `app/Resources/Themes/`.  Se avete
necessità di modificare l'aspetto dei vostri libri **non** dovete modificare i
file che si trovano in quste cartelle. Il prossimo capitolo spiegherà come
sovrascrivere ogni struttura o risorsa per i vostri libri.

### Contenuti predefiniti ###

In molti libri gli unici elementi che vengono definiti sono capitoli e
appendici (con l'opzione `content`). In aggiunta, **easybook** definisce dei
contenuti predefiniti per alcuni tipi di contanuto. Se il vostro libro, per
esempio, include una pagina iniziale (tipo di contenuto `title`) senza nessun
file con contenuto:

    [yaml]
    book:
        # ...
        contents:
            - ...
            - { element: title }
            - ...

**easybook** utilizzerà il seguente come contenuto per questo elemento:

    [twig]
    <h1>{{ book.title }}</h1>
    <h2>{{ book.author }}</h2>
    <h3>{{ book.edition }}</h3>

La pagina del titolo predefinita mostrerà il titoolo, il nome dell'autore e
l'edizione corrente del libro. Tutti qesti valori sono configurati
nell'opzione `book` del file `config.yml`.

I contenuti definiti da **easybook** dipendono sia dal tipo di contenuto che
dall'edizione in cui devono essere pubblicati. Potete accedere a questi valori
predefiniti nella cartella  `Contents/` del tema.

### Contenuti predefiniti ###

Se non volete usare i contenuti predefiniti di **easybook** per alcuni
elementi, aggiungete semplicemente l'opzione `content` che indica il file che
definisce questo contenuti:

    [yaml]
    book:
        # ...
        contents:
            - ...
            - { element: license, content: creative-commons.md }
            - { element: title, content: my-own-title-page.md }
            - ...

### Strutture predefinite ###

Il contenuto di ogni elemento è *decorato* con una struttura prima di essere
incluso nel libro pubblicato. Le strutture di **easybook** sono realizzate con
[Twig](http://twig.sensiolabs.org/), il miglior libguaggio di templating per
PHP. Voi potete accedere a tutte le strutture predefinite nella cartella
`Templates/` del tema.

Guardiamo per esempio la struttura usata per decorare ogni capitolo di un
libro in PDF:

    [twig]
    <div class="page:chapter new-page">

    <h1 id="{{ item.slug }}"><span>{{ item.label }}</span> {{ item.title }}</h1>

    {{ item.content }}

    </div>

I dati del contenuto che devono essere decorati sono accessibili attraverso
una variabile speciale chiamata `item`, che ha le seguenti proprietà:

  * `item.title`, è il titolo del contenuto. E' ottenuto dall'opzione di
  configurazione `title`, dal contenuto o dal valore predefinito di
  **easybook**.
  * `item.slug`, è la versione *sicura* del `title` e non include spazi o ogni
  altro *carattere pericoloso* (aome accenti, `.`, `?`, `!`, ...). Questo
  valore è usato per gli URLs, nell'attributo HTML `id`, etc.
  * `item.label`, l'etichetta della sezione proncipale del contenuto.
  Solitamente è definita solo per capitoli (`Capitolo XX`), parti (`Parte XX`)
  e appendici (`Appendice XX`).
  * `toc`, un array con l'indice dei contenuti di questo elemento. E' vuoto
  per la paggior parte dei tipi di contenuto (`cover`, `license`, etc.) ma può
  essere molto grande e complesso per elementi complessi come capitoli ed
  appendici.
  * `item.content`, il contenuto dell'elemento preparato per essere incluso
  nel libro (è già stato convertito dal formato Markdown originale).
  * `item.original`, Il contenuto originale dell'elemento senza nessuna
  modifica.
  * `item.config`, array con tutte le opzioni di configurazione definite per
  l'elemeto nel file `config.yml`. Internamete sono presenti le proprietà
  `number`, `title`, `content` e `element`. Per esempio, potete accedere al
  tipo di elemento con la seguente espressione: `{{ item.config.element }}`.

Immagini e tabelle sono decorate con una struttura speciale chiamata
`figure.twig` e `table.twig` che ha acccesso alle seguenti variabili:

   * `item.caption`, è il titolo dell'immagine/tabella indicata nel contenuto
   originale.
   * `item.content`, è il codice HTML completo generato per visualizzare
   l'immagine/tabella nel libro (`<img src="..." alt="..." />` o
   `<table> ... </ table>`).
   * `item.label`, l'etichetta dell'immagine/tabella. Questo valore è vuoto
   intanto che l'opzione `labels`dell'edizione include `figure` e/o `table`.
   * `item.number`, è un numero autogenerato dell'immagine/tabella
   correntemente elaborata. La prima immagine/tabella avrà il numero `1` e le
   seguenti saranno aumentate di uno.
   * `element.number`, è il numero dell'elemento padre (capitolo, appendice,
   etc.) della immagine/tabella. Questa proprietà verrà usata per anteporre,
   per esempio, `5` per tutte le immagini/tabelle incluse nel capitolo `5` del
   libro.

In aggiunta a queste proprietà, tutte le strutture di **Easybook** hanno
accesso a tre variabili globali:

  * `book`, fornisce accesso diretto alle opzioni di configurazione definite
  sotto `book` nel file `config.yml`. Potete accedere, per esempio, all'autore
  del libro in ogni struttura usando `{{ book.author }}` e la versione di
  **easybook** corrente usando `{{ book.generator.version }}`.
  * `edition`, fornisce accesso diretto alle opzioni di configurazione
  dell'edizione che è correntemente in pubblicazione.
  * `app`, fornisce accesso diretto a tute le opzioni di configurazione e servizi di **easybook** (definiti nel file `src/DependencyInjection/Application.php`).

### Custom templates ###

In the next chapter you'll learn how to use your own templates instead of
**easybook** default templates.

### Default styles ###

The appearance of the books is defined by CSS stylesheets, even in the case of
`epub` and `pdf` type editions. **easybook** includes several default styles in
the `Templates/` directory of the theme. CSS styling in `epub` editions is pretty
limited due to the absymal support of most e-book readers.

For `html` and `html_chunked` editions, the limit is the highest CSS version that
you can use on your website (CSS 2.1, CSS 3, CSS 4, etc..) because every modern
web browser offers an excelent CSS support.

In the case of `pdf` editions, your imagination is the only limit. PDF books are
generated by [PrinceXML](http://www.princexml.com/) transforming a HTML document
into a PDF file using a CSS stylesheet. PrinceXML defines tens of new CSS
properties and options unavailable in the CSS standards. Using these exclusive
properties you can easily add amazing features to your book design and layout.
We strongly recommend you take a look at the `styles.css.twig` file of the `Pdf/`
theme to learn some of the most advanced features. It will blow your mind away!
And don't forget to read [PrinceXML documentation](http://www.princexml.com/doc/8.0/).

### Custom styles ###

In the next chapter you'll learn how to use your own CSS styles instead of
**easybook** default styles.

### Default fonts ###

**easybook** bundles several free and high-quality fonts to make published books
look professional. You can see the fonts and their license in the
`app/Resources/Fonts/` directory.

### Default labels and titles ###

**easybook** requires each content to have its own title.  Chapters and appendices
include the title within their own content as the first section heading and parts
define it in the `title` option of the `config.yml` file. For the rest of content
types, **easybook** assigns a default title that varies depending on the language
in which the book is written. You can see the titles applied to English books in
`app/Resources/Translations/titles.en.yml`.

Moreover, the book can add labels (`Chapter XX`, `Appendix XX`, etc.) to section
titles using the `labels` option. As explained before, this option indicates the
content types for which tags are added automatically. By default the book only
adds tags in chapters and appendices. The default labels applied to books written
in English are defined in `app/Resources/Translations/labels.en.yml` file.

Unlike the titles, labels can contain variable parts, such as the appendix or
chapter number. Therefore, **easybook** uses Twig templates to define each label:

    [yaml]
    label:
        figure: 'Figure {{ element.number }}.{{ item.number }}'
        part:   'Part {{ item.number }}'
        table:  'Table {{ element.number }}.{{ item.number }}'

The templates for `figure` and `table` labels can use the same variables as
`figure.twig` and `table.twig` templates explained before. Therefore,
`{{ item.number }}` shows the autogenerated number of the image/table and
`{{ element.number }}` shows the number of the chapter or appendix.

Chapters and appendices must define six different labels, each corresponding to
one of the six heading levels (`<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>` and `<h6>`).
In the following example, appendices only include a label in their titles, thus
leaving empty the last five levels:

    [yaml]
    label:
        appendix:
            - 'Appendix {{ item.number }}'
            - ''
            - ''
            - ''
            - ''
            - ''

Labels can access to all configuration options defined by the item in the
`config.yml` file. The label of a chapter can then use `{{ item.number }}` to
show the number of the chapter. In addition to these properties, label templates
have access to two special variables called `level` and `counters`.

The `level` variable indicates the section heading level for which you want to
get the label, being `1` the level of `<h1>` heading and `6` the level of `<h6>`
headings. The `counters` variable is an array with the counters of all heading
levels. For that reason, to show second-level headings as `1.1`, `1.2` ... `7.1`,
`7.2` you can use the following expression:

    [yaml]
    label:
        chapter:
            - 'Chapter {{ item.number }}'
            - '{{ item.counters[0] }}.{{ item.counters [1] }}'
            - ...

Extending the previous example, you can use the following templates to format
all the heading levels as `1.1`, `1.1.1`, `1.1.1.1`, etc.:

    [yaml]
     label:
         chapter:
             - 'Chapter {{ item.number }} '
             - '{{ item.counters[0:2]|join(".") }}'  # 1.1
             - '{{ item.counters[0:3]|join(".") }}'  # 1.1.1
             - '{{ item.counters[0:4]|join(".") }}'  # 1.1.1.1
             - '{{ item.counters[0:5]|join(".") }}'  # 1.1.1.1.1
             - '{{ item.counters[0:6]|join(".") }}'  # 1.1.1.1.1.1

This last example clearly shows what you can achieve by combining the
flexibility of **easybook** and the power of Twig.

### Custom labels and titles ###

If you want to use your own titles and labels, you must first create the
`Translations` directory inside the `Resources` directory of your book (you must
also create the latter if it doesn't exist). Then add the new label file in one
of the following directories:

   1. `<book>/Resources/Translations/<edition-name>/labels.en.yml`, if you want
   to change the labels in a single edition. The subdirectory of `Translations`
   must be named exactly like the edition being published.
   2. `<book>/Resources/Translations/<edition-type>/labels.en.yml`, if you want
   to change the labels in all editions of the same type. The directory in
   `Translations` can only be named `epub`, `html`, `html_chunked` or `pdf`.
   3. `<book>/Resources/Translations/labels.en.yml`, if you want to change the
   labels on all the editions of the book, regardless of its name or type.

When you use your own label file, you don't have to define the value of all
labels. Add only the labels that you want to modify and **easybook** will assign
to the rest their default values. Therefore, to only modify the label of the
images in any book edition, create a new `<libro>/Resources/Translations/labels.en.yml`
file and add just the following content:

    [yaml]
    label:
        figure: 'Illustration {{ item.number }}'

If you want to change the titles instead of the labels, follow the same steps
but create a file called `titles.en.yml` instead of `labels.en.yml`. If your book
isn't written in English, replace `en` for the code of the other language (e.g.
`labels.es.yml` for Spanish labels).
