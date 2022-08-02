# Gestione dello staging in Git

La gestione dello staging è probabilmente una delle fasi più articolate per quanto riguarda le procedure di versioning con Git, l'area di stage rappresenta infatti una sorta di entità intermedia tra la directory di lavoro e la directory del DVCS; una volta eseguite le operazioni relative allo staging, sarà possibile effettuare il commit delle modifiche apportate al proprio progetto, tenendo a mente però che qualsiasi elemento unstaged, cioè qualunque file che sia stato creato o modificato senza essere stato passato come argomento a git add, non potrà essere committato.

## Staging e tracciamento

a modifica dei file già tracciati rappresenta un intervento abbastanza frequente nel controllo di versione, a questo proposito rimangono però da chiarire le implicazioni di tale processo sullo staging; l'esempio mostrato nell'immagine seguente fa riferimento all'eventualità di un cambiamento apportato al file denominato NOTES, progetto MyWP, che era stato già sottoposto a commit nel capitolo precedente:

![](https://static.html.it/app/uploads/2015/09/f1.png)

Nel caso specifico l'elemento di novità è rappresentato dalla notifica "Changed but not staged for commit", sostanzialmente ci si trova a dover gestire un file in piena fase di tracciamento che ha subito una modifica nella directory di lavoro ma non è stato ancora sottoposto a staging; l'ingresso in area di stage sarà possibile anche in questo caso tramite l'utilizzo dell'istruzione git add che, come risulta ormai chiaro, non viene chiamato in causa soltanto per il tracciamento e lo staging di file addizionali e permette di lavorare anche su risorse preesistenti adottando la medesima sintassi.

Una volta passato il nome del file come argomento al comando per lo staging si potrà effettuare un'ulteriore verifica sullo stato del progetto che dovrebbe confermare l'assenza di file al di fuori dell'area di stage:

```
git add NOTES
git status
```

## Staging e modifiche addizionali
Come anticipato, il caso precedentemente esposto è tutt'altro che raro, meno frequente, ma non per questo irrilevante, è l'eventualità che prevede di apportare ulteriori modifiche ad un file che ha già subito un cambiamento prima che quest'ultimo sia stato coinvolto in un commit. A tal proposito è possibile presentare un esempio, rappresentato nell'immagine successiva, che mostra il risultato di una verifica di stato eseguita dopo un secondo intervento di editing del file NOTES.

![](https://static.html.it/app/uploads/2015/09/f2.png)

Non è necessario vantare una lunga esperienza nell'uso di Git per notare come l'output prodotto dall'ennesima esecuzione di git status contenga dei dati in apparente contraddizione tra loro, infatti NOTES risulta essere nello stesso tempo sia un file "modificato" che "non modificato" e, cosa ancora più interessante dal punto di vista del versioning, viene indicato contemporaneamente come staged e non in staging. Quali le ragioni di tale incoerenza?

Per rispondere a questa domanda bisognerebbe fare nuovamente riferimento alla funzione svolta dall'istruzione git add o, per meglio dire, alle sue funzioni. Lo stage rappresenta una sorta di indice per un progetto prima del passaggio alla directory di Git, motivo per il quale git status mostrerà lo stato di quest'area fornendo un risultato fedele a quello generato dall'esecuzione dell'ultima chiamata a git add.

L'implicazione più rilevante di tale comportamento è rappresentata dal fatto che senza il ricorso a git add l'ulteriore modifica al file non prenderà parte ad un eventuale commit perché non registrata in stage, ne consegue che a passare nella directory di Git sarà soltanto la versione del file precedente a tale intervento. Sia chiaro quindi che per ottenere la sincronizzazione tra la propria working directory e quella di Git sarà necessario richiamare git add per lo staging di ciascuna modifica eseguita sul file coinvolto. Nel dubbio sarà sempre possibile ricorrere a git status per verificare che nessun file sia associato alla dicitura "Changes not staged for commit".

## git diff come alternativa a git status

Uno dei grandi limiti di git status sta nel fatto che esso permette di identificare i file che hanno subito delle modifiche ma non consente di capire quali cambiamenti siano stati apportati ad esso; per colmare tale lacuna si è scelto di fornire un comando in grado di produrre output nettamente più particolareggiati: git diff. Un semplice esempio di utilizzo di quest'ultimo potrebbe essere quello raffigurato nell'immagine seguente, dove il già più volte manipolato NOTES subisce un ulteriore intervento.


Come è possibile notare, il risultato della chiamata all'istruzione mostra rispettivamente in rosso e in verde la precedente modifica ormai già in stage e quella appena effettuata senza il successivo staging tramite git add; nel caso in cui non dovessero essere presenti modifiche da registrare in area di stage git diff non produrrà alcun output, perché non vi saranno differenze tra il file NOTES contenuto nella directory di lavoro e quello nello stage.

Sempre a proposito di questo comando, l'utilizzatore dovrà ricordare che git diff non si occupa di mostrare tutte le modifiche eseguite a partire dall'ultimo commit effettuato, esso infatti permetterà di visualizzare i soli cambiamenti non ancora in stage quando presenti.

## Evitare il transito nell'area di stage

Per quanto importantissima ai fini della revisione in fase di implementazione di un progetto, l'area di stage potrà essere bypassata evitando quindi che un file modificato transiti attraverso di essa. Tale risorsa verrà trasferita dalla working directory a quella di Git associando alla già citata istruzione git commit -m l'argomento -a:

```
$ git commit -a -m 'Bypassing staging'


```
Anche nel caso in cui un file dovesse aver subito delle modifiche senza una successiva chiamata a git add, l'opzione -a garantirà che una successiva esecuzione di git status o git diff non segnalino la presenza di cambiamenti non registrati in area di stage.

