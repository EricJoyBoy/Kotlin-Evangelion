# Operazioni sui file con Git

Git mette a disposizione alcune funzionalità grazie alle quali eseguire semplici operazioni per la gestione dei file, tramite il DVCS essi potranno essere ignorati quando di secondaria importanza rispetto all'economia di un'applicazione, spostati o cancellati influenzando direttamente l'evoluzione di un progetto e le esigenze legate al versioning per la sua implementazione.

## Definire i file da ignorare

Non tutti i file appartenenti ad un progetto sono indispensabili per le attività di sviluppo e controllo di versione, si pensi per esempio ai logs prodotti automaticamente dai test di funzionamento delle applicazioni, dalle sessioni per il debugging o dai benchmarks, questi ultimi infatti non prendono parte alla struttura di un software e possono variare a seconda dell'ambiente di riferimento. Volendo evitare che tali risorse prendano parte al flusso di dati che dalla working directory vengono veicolati fino alla directory di Git, la soluzione migliore sarà quella di creare delle apposite liste di esclusione.

Nel DVCS tali elenchi prendono il nome di .gitignore, essi possono contenere dei patterns che consentono di stabilire tramite singole istruzioni quali gruppi di file dovranno essere ignorati, come per esempio nel caso dei file temporanei prodotti dagli editor durante le attività di modifica delle risorse coinvolte; quanto indicato in .gitignore avrà effetto su tutte le directory di un progetto, a meno che esse non presentino a loro volta una propria lista di esclusione.

L'esempio seguente mostra innanzitutto l'istruzione per la creazione di .gitignore e, successivamente, la direttiva con la quale sarà possibile ignorare tutti i file caratterizzati da una specifica estensione; si noti inoltre il ricorso alla wildcard * che permetterà di non dover specificare uno per uno i nomi completi dei file da ignorare:

```
$ cat .gitignore
# ignora tutti i file con estensione .log
*.log
```

## Definire patterns per .gitignore

Chiaramente è anche possibile creare dei patterns articolati e inserire più direttive in una stessa lista, come nel caso del .gitignore seguente che consentirà di ignorare tutti i file che finiscono per "x", "y" o tilde ("~"):

```
$ cat .gitignore
# ignora tutti i file che finiscono con le lettere specificate
*.[xy]
# ignora tutti i file che finiscono con un simbolo specifico
*~

```

La sintassi prevista permette di operare anche su intere directory e su tutto il loro contenuto, nel caso specifico dell'esempio proposto di seguito verranno ignorate tutte le cartelle, le sottocartelle e i file presenti all'interno della directory tmp mentre, per quanto riguarda logs, verranno ignorati i soli file:


```
$ cat .gitignore
# ignora directory e sottodirectory della cartella tmp
tmp/**/*
# ignora tutti i file contenuti nella cartella logs
logs/

```

* non è l'unico elemento (glob pattern) disponibile per la definizione dei patterns, si potrà utilizzare per esempio ! per evitare che un determinato file venga ignorato:


```
$ cat .gitignore
# ignora tutti i file HTML
*.html
# tranne index.html
!index.html

```

Nello stesso modo / consentirà di gestire anche le omonimie tra file e cartelle o le esclusioni interne a queste ultime:


```
$ cat .gitignore
# ignora tutti i file HTML
*.html
# tranne index.html
!index.html

```

Utilizzando ? si potranno ignorare file i cui nomi contengono singoli caratteri, così come con [0-9] o varianti di tale intervallo verranno ignorati i file che presentano caratteri compresi all'interno di esso, mentre verranno ignorate le righe vuote o le direttive precedute da # in quanto considerate dei commenti. Le combinazioni disponibili sono quindi numerose, si ricordi però che il fatto di inserire in .gitignore un file già tracciato non lo escluderà automaticamente da tale attività.

## Cancellazione dei file

La cancellazione di un file richiede in Git una procedura abbastanza semplice basata sul comando git rm, ma è comunque interessante osservare quale sia l'effetto di tale operazione sull'economia di un progetto; in sostanza un file da cancellare dovrà essere rimosso dall'area di stage in modo da escluderne il tracciamento, fatto questo tale intervento dovrà essere committato e si otterrà la sua cancellazione anche dalla directory di lavoro.

Per comodità dell'utilizzatore git rm, a cui dovrà essere passato come argomento il nome del file da eliminare, si occuperà di effettuare tutti i passaggi precedentemente esposti, come evidenziato dalla figura successiva:

![](https://static.html.it/app/uploads/2015/09/g1.png)

git rm supporta l'utilizzo di patterns e wildcards per l'eliminazione delle risorse, a tal proposito i due esempi proposti di seguitano mostrano rispettivamente come cancellare tutti i file dotati di una specifica estensione e tutti i file presenti in una determinata cartella dotati della medesima estensione; si osservi l'utilizzo del backslash prima dell'asterisco, necessario per il corretto funzionamento delle istruzioni.


```
$ git rm \*.txt

```

```
$ git rm docs/\*.txt

```

Può capitare che un utilizzatore voglia cancellare un file dall'area di stage conservandolo però nella directory di lavoro, ciò sarà possibile grazie all'opzione --cached che porrà fine al tracciamento del file passato come argomento senza eliminarne la copia locale; quest'ultima in futuro potrà essere riportata in stage tramite git add.

![](https://static.html.it/app/uploads/2015/09/g2.png)

Nel caso in cui si cancelli un file manualmente dalla directory di lavoro, git status lo identificherà come modificato ma non aggiornato, i cambiamenti non risulteranno quindi in staging e si dovrà comunque procedere con una chiamata a git rm; tale intervento verrà registrato nel directory di Git in coincidenza con il commit successivo.

## Spostamento dei file

A titolo di esempio si crei nella propria working directory una nuova cartella denominata backup, fatto questo si sposti il file NOTES all'interno di quest'ultima tramite un'istruzione basata sul comando mv modificandone contemporaneamente il nome in NOTES_BK:

```
$ mv NOTES backup/NOTES_BK

```


Per riportare il file nella sua posizione originale e rinominarlo come in precedenza basterà rispettare la medesima sintassi e i percorsi interni alla propria area di lavoro

```
$ cd backup/
$ mv NOTES_BK ../NOTES

```

Si noti come mv permetta di eseguire sia operazioni di spostamento che di rinomina dei file; un file sottoposto a tracciamento lo sarà anche una volta spostato, ma perché tale modifica venga memorizzata anche nella directory di Git sarà necessario un commit; in ogni caso Git non archivierà l'informazione relativa al fatto che un file sia stato rinominato.