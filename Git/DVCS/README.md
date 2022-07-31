#  Git e il controllo di versione distribuito

## Il controlllo di versione

Il controllo di versione (versioning) è sostanzialmente un meccanismo attraverso il quale tenere traccia con il passare del tempo delle modifiche apportate ad un progetto; quest'ultimo può essere costituito da un singolo file o da un insieme di file le cui diverse versioni vengono registrate e possono essere richiamate in un momento successivo, anche a grande distanza di tempo, ogni volta che se ne presenti la necessità.

In linea generale, si tende ad associare il concetto di controllo di versione allo sviluppo di applicazioni e all'implementazione delle differenti release, tuttavia è possibile applicare il versionig anche a progetti di natura differente, come per esempio la documentazione relativa ad un sistema o a un linguaggio, le specifiche associate a uno standard, una cronologia, un layout grafico (si pensi per esempio all'evoluzione di un logo), nel complesso, qualsiasi file sia suscettibile di modifiche.

Nello specifico dello sviluppo software, ma il discorso potrebbe essere ampliato ad altri ambiti di utilizzo, l'impiego di un sistema per il controllo di versione consente di semplificare il lavoro di un team, fornendo ai suoi componenti gli strumenti per monitorare i cambiamenti effettuati da terzi ad ogni revisione, per risalire ad un intervento che potrebbe aver causato un malfunzionamento, per annullare una variazione ripristinando la precedente release di un file o di un progetto nel suo insieme.

Esistono diverse modalità per controllo di versione: dal semplice monitoraggio locale a sistemi centralizzati, fino al versioning distribuito proprio di Git. Comprendere le differenze tra questi approcci aiuterà a scegliere quello più adatto per le prorpie esigenze.

## Controllo di Versione Locale

Il controllo di versione locale è la forma più essenziale e primitiva di versioning; si immagini uno sviluppatore che crea un'applicazione, effettua la presentazione o la messa in produzione di quest'ultima e poi, magari su suggerimento del committente, effettua delle modifiche introducendo aggiornamenti e correzioni. In questo caso le diverse versioni del progetto potrebbero essere salvate in differenti cartelle rinominate, ad esempio associando la data dell'ultima modifica effettuata al nome del progetto.

lmeno in teoria tale approccio non necessita di un software per la gestione delle diverse relese, ma cosa potrebbe accadere nel caso di progetti articolati coinvolti da numerose modifiche? Tenere traccia degli interventi effettuati diventerebbe complesso con il rischio di perdere molte informazioni con il passare del tempo e l'accumularsi degli interventi eseguiti. Ecco perché vennero ideate le prime soluzioni per il versiong come per esempio il free software RCS (Revision Control System), queste ultime funzionano grazie ad un database destinato a registrare le modifiche apportate ai file e tramite delle patch che memorizzano le differenze tra le revisioni in modo da semplificare le operazioni di ripristino.

Sistemi come RCS facilitano il controllo di versione locale ma offrono strumenti limitati per lo sviluppo in ambito collaborativo, motivo per il quale si cercò una soluzione a tale problematica ricorrendo ai CVCS (Centralized Version Control Systems).

## Controllo di versione centralizzato

I sistemi centralizzati per il controllo di versione (chi li adotta conoscerà sicuramente Subversion), sono caratterizzati dal fatto di funzionare sulla base di un singolo server a cui viene affidato il compito di ospitare tutte le varianti dei progetti sottoposti a versioning, tale server permetterà quindi anche il download dei file da parte degli utenti interessati a partecipare allo sviluppo, a creare dei fork (versioni derivate dal sorgente di un progetto originale) o semplicemente ad utilizzare una determinata applicazione.

![](https://static.html.it/app/uploads/2015/03/IMG_25032015_144045.png)


Tali sistemi offrono degli indubbi vantaggi rispetto a quelli per il controllo di versione locale, soprattutto in considerazione del fatto che in un contesto che prevede la partecipazione di più soggetti sarà più facile tenere traccia delle modifiche apportate da altri; questo senza contare il ruolo fondamentale svolto dagli amministratori a cui viene data la possibilità di accordare diversi privilegi di accesso e scrittura ai file ad utenti differenti.


La dinamica descritta è possibile grazie ad un'apposita funzionalità per la creazione di backup completi denominata checkout dei repository, essa in pratica consente di generare una copia di un repository locale o di un server remoto tramite un comando per la sua clonazione.

A rendere vantaggioso un approccio basato sul controllo di versione distribuito è anche il superamento dell'impostazione "gerarchica" propria dei sistemi centralizzati, un limite a carico del livello di produttività che potrebbe rivelarsi determinante nella gestione del flusso di lavoro; i DVCS come Git permettono infatti di operare su più repository in remoto, in questo modo si avrà la possibilità di lavorare in contemporanea sul medesimo progetto con gruppi di collaboratori differenti seguendo diverse metodologie.