# Android Studio


Android Studio deriva da IntelliJ di JetBrains, un IDE per il mondo Java particolarmente sensibile alle necessità dello sviluppatore. Al suo interno, include però Gradle, un ottimo strumento per la build automation, molto flessibile ed erede di tutte le principali caratteristiche di predecessori come Apache Ant e Maven.

All'avvio, l'IDE mostra una finestra di benvenuto, sulla sinistra della quale troviamo un elenco di progetti aperti di recente, mentre sulla destra è presente un menu che permette l'avvio del lavoro in varie modalità. Selezioniamo la voce Start a new Android Studio project.

La creazione guidata che viene avviata si articola in due schermate:

 - la prima permette di scegliere la tipologia di applicazione. Innanzitutto, definiamo il contesto applicativo tra
Phone e Tablet, Wear OS, TV, Android Auto e Android Things. Per ognuna
di queste verrà proposta una serie di modelli di base ma noi, in questa guida, ci concentriamo principalmente sulla prima
tipologia. Qui supporremo di aver selezionato il modello "Empty Activity";

- nella seconda schermata configuriamo il progetto scegliendo il nome dell'app, il package, la collocazione nel
file system della macchina di sviluppo, il linguaggio di programmazione tra Java e Kotlin e la versione minima delle
API Android da supportare.


Al termine di questa procedura ci verrà fornito un semplice progetto, in stile "Hello World", perfettamente funzionante.

## Struttura di un progetto in Android Studio

Anche su Android Studio troveremo tre parti principali del progetto: la cartella con il codice Java, la cartella res (contenente risorse per lo più realizzate in XML) ed un file di configurazione denominato AndroidManifest.xml. La figura seguente mostra la disposizione di tali elementi.



![](https://static.html.it/app/uploads/2015/04/guidaandroid_06bis_img_01.jpg)

Per prima cosa, si noti che il progetto è contenuto in una cartella denominata app. Questo è il modulo di default. L'IDE, infatti, suddivide un progetto in più moduli, ognuno dei quali può svolgere un ruolo diverso (libreria Java, libreria Android, inclusione di un progetto esterno, eccetera...). Il modulo app include i file manifest, il codice Java e le risorse.

Dopo il modulo troviamo la sezione Gradle Scripts. Qui ci sono i file di build che userà Gradle per trasformare il nostro progetto in un'app funzionante. In particolare, i file di build sono due: uno per tutto il progetto ed uno per il solo modulo app. Vediamo di seguito quest'ultimo, che è quello tipicamente modificato dal programmatore.

``` java
apply plugin: 'com.android.application'
android {
    compileSdkVersion 29
    buildToolsVersion "29.0.2"
    defaultConfig {
        applicationId "it.html.helloworld"
        minSdkVersion 15
        targetSdkVersion 29
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}

```


La prima riga carica il plugin Gradle per android. Questo permette di avere a disposizione la sezione seguente contenuta nella direttiva android { ... }. Al suo interno vengono impostati alcuni fattori che nei progetti Eclipse trovano spazio nel file AndroidManifest.xml: minimo SDK cui l'app è destinata (minSdkVersion), SDK target (targetSdkVersion), versione di sviluppo (versionCode) e versione pubblica (versionName).

La sezione successiva denominata dependencies, è molto importante per l'espansione delle funzionalità del progetto.

La riga seguente:


``` java
implementation fileTree(dir: 'libs', include: ['*.jar'])

```

include nel build path tutti i file .jar che trova nella cartella libs, mentre la riga:

```java
implementation 'androidx.appcompat:appcompat:1.1.0'

```

include nel progetto la libreria AndroidX Appcompat che offre compatibilità con le versioni precedenti del sistema operativo.
AndroidX, parte del framework Jetpack che contempla
tutti i principali strumenti di sviluppo Android, sostituisce la Support Library che per molti anni ha svolto il medesimo ruolo.

È interessante notare come sia espresso il nome della dipendenza. Esso è costituito da tre parti, separate dal simbolo :. Questo tipo di espressione richiama il formato di Maven: androidx.appcompat è l'identificativo del gruppo di sviluppo, appcompat il nome del progetto da includere e 1.1.0 è la versione del progetto.

## SDK Manager ed emulatori su Android Studio

Il menu Tools presenta le voci AVD Manager e SDK Manager che permettono di attivare,
rispettivamente, Android SDK Manager e Android Virtual Device Manager.

Il primo, come accennato nelle lezioni precedenti, è il pannello per integrare il proprio SDK con ulteriori funzionalità ed aggiornamenti.

Il secondo permette di creare uno o più emulatori, qualora non si vogliano o non si possano eseguire i propri progetti direttamente su dispositivo reale. Il pannello che lo costituisce presenta, in basso, il pulsante Create Virtual Device..., selezionando il quale verrà avviata la creazione di un emulatore, del quale si potranno scegliere modello e caratteristiche. Terminata la creazione, il nuovo emulatore apparirà nella finestra Your Virtual Devices e da lì potrà essere avviato.

##  Design di layout

Un aspetto significativo di Android Studio consiste nell'anteprima di layout praticamente istantanea. Se si apre un file contenente la stuttura del layout – reperibile, ad esempio, nella cartella res/layout - si vede che il suo contenuto può essere mostrato in modalità Design (visuale, incluso nel display di un dispositivo) oppure Text, che mostra il tipico formato XML.

Il pannello Design può essere utile per visualizzare rapidamente le modifiche apportate al sorgente XML, oppure per disegnare in modalità visuale l'interfaccia, trascinando, direttamente sul display, controlli utente dalla Palette.

Inoltre, il pannello Design presenta alcuni menu a tendina che permettono di modificare le condizioni dell'anteprima in termini di modello, orientamento e versione di Android disponibile.

![](https://static.html.it/app/uploads/2017/07/guidandroid-07-img-design.jpg)