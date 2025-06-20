<br>

<br>
## SNAKE

Questo progetto è una semplice implementazione del classico gioco Snake, sviluppato in linguaggio C e compilato con Emscripten per poter essere eseguito direttamente nel browser tramite WebAssembly.

Il gioco è stato creato per imparare come integrare codice C in una pagina web moderna, sperimentare con Emscripten e approfondire la logica di gioco.
È rivolto a chiunque voglia scoprire come funziona un gioco Snake “dietro le quinte”, agli appassionati di programmazione e a chi vuole vedere come il C può essere portato sul web.

## **Motivazione**

Sono sempre stato affascinato dalla possibilità di portare codice scritto in linguaggi “tradizionali” come il C sul web.
Per questo motivo ho scelto di sviluppare Snake usando Emscripten, così da sperimentare in prima persona come funziona la compilazione di codice C in WebAssembly e come si integra con una pagina web moderna.
Il gioco Snake, semplice ma completo, mi ha permesso di mettere in pratica la logica di gioco e di approfondire la gestione degli input e del rendering.

## Tecnologie Utilizzate

* **C:** Linguaggio principale utilizzato per sviluppare la logica di gioco.
* **SDL (Simple DirectMedia Layer):** Libreria cross-platform per la gestione di grafica, audio e input, utilizzata per il rendering e la gestione degli eventi.
* **SDL\_ttf:** Libreria per la gestione dei font in SDL.
* **Emscripten:** Toolchain per la compilazione di codice C in WebAssembly, che permette di eseguire il gioco nel browser.
* **WebAssembly:** Formato binario per l’esecuzione efficiente di codice nativo nel browser.
* **HTML/JavaScript:** Utilizzati per la pagina web che ospita il gioco e per integrare il codice WebAssembly.

## **Architettura e Scelte Progettuali**

* **Perché hai usato Emscripten?**

Ho scelto di utilizzare **Emscripten** per poter portare il gioco Snake, sviluppato in C, direttamente nel browser web.
Emscripten è una toolchain che permette di compilare codice C/C++ in WebAssembly, un formato binario eseguito in modo efficiente dai browser moderni.

Questa scelta offre diversi vantaggi:

* **Portabilità:** Il gioco può essere eseguito da chiunque abbia un browser moderno, senza bisogno di installare nulla.
* **Riuso del codice:** Posso mantenere la logica di gioco scritta in C, integrando solo le parti necessarie per il web.
* **Performance:** WebAssembly garantisce performance vicine a quelle native, ideali per un gioco come Snake.
* **Supporto a librerie grafiche:** Emscripten supporta SDL, permettendomi di continuare a usare le funzioni grafiche e di input che già conosco.

In sintesi, Emscripten mi ha permesso di sperimentare come integrare codice C in una pagina web moderna, dimostrando una visione proattiva e orientata al futuro.

* **Perché hai scelto di implementare Snake in C invece che in JavaScript?**

La decisione di sviluppare Snake in C nasce dal desiderio di approfondire la conoscenza del linguaggio e di sperimentare la portabilità di un’applicazione tradizionale sul web moderno.
Implementare il gioco in C mi ha permesso di consolidare la comprensione della gestione della memoria e della logica di programmazione a basso livello, oltre a offrirmi l’opportunità di esplorare strumenti come Emscripten per la compilazione in WebAssembly.

#### Vantaggi dell’uso del C

* **Controllo fine:** Il C offre un controllo dettagliato sulla memoria e sulle risorse.
* **Performance:** Il codice C compilato è generalmente più veloce rispetto a JavaScript per operazioni critiche.
* **Portabilità:** Grazie a toolchain come Emscripten, il codice C può essere eseguito su molte piattaforme, inclusi i browser web.
* **Formazione:** Lavorare in C è un’ottima palestra per comprendere i principi fondamentali della programmazione.

#### Svantaggi dell’uso del C

* **Complessità:** Il C richiede una maggiore attenzione alla gestione della memoria e alla prevenzione di errori.
* **Integrazione con il web:** L’integrazione di codice C in una pagina web richiede strumenti aggiuntivi e una fase di compilazione.
* **Debugging:** Il debugging di codice C compilato per il web può essere più complesso.


**Quali problemi hai riscontrato durante lo sviluppo e come li hai risolti?**

Durante lo sviluppo del gioco Snake in C, ho incontrato diverse sfide tecniche, soprattutto nella gestione della logica di gioco e nell’integrazione con il web tramite Emscripten.

**Logica di ingrandimento del serpente:**
Inizialmente, la nuova parte del corpo veniva aggiunta in coda, causando problemi di visualizzazione e di movimento.
Ho risolto modificando la struttura dati che rappresenta il serpente, aggiungendo la nuova parte in testa e spostando tutto il corpo di conseguenza.
Questo approccio ha reso il movimento del serpente più naturale e coerente con il funzionamento classico del gioco.

**Portabilità su sito web:**
Ho riscontrato difficoltà nella configurazione degli strumenti di compilazione e nella gestione degli asset.
Ho studiato la documentazione di Emscripten e delle librerie SDL, seguendo esempi e tutorial per configurare correttamente il progetto e gestire gli asset tramite la virtualizzazione del filesystem di Emscripten.

**Bug vari:**
Durante lo sviluppo, ho incontrato diversi bug minori, come problemi nella gestione degli input o nel rendering grafico.
Ho adottato un approccio sistematico al debugging, utilizzando strumenti come printf, debugger e test manuali per identificare e correggere gli errori.

## Come Funziona il Progetto

Breve spiegazione di come funziona il gioco:

* **Logica di gioco**
* **Input dell’utente**
* **Rendering grafico**


### Logica di gioco

Il gioco Snake si basa su una struttura dati che rappresenta il serpente come una lista di segmenti, ciascuno corrispondente a una posizione sullo schermo.  
La posizione iniziale del serpente è definita all’avvio del gioco, tipicamente al centro dello schermo.

- **Movimento:**  
  Il serpente si muove in una delle quattro direzioni principali (su, giù, sinistra, destra).  
  Ad ogni frame, la testa del serpente si sposta nella direzione corrente, mentre ogni segmento del corpo segue il segmento precedente.  
  Questo meccanismo è realizzato aggiornando le coordinate di ogni segmento a partire dalla coda fino alla testa, oppure aggiungendo la nuova parte in testa e rimuovendo la coda (a seconda dell’implementazione).

- **Crescita:**  
  Quando il serpente raccoglie il cibo (rappresentato da un elemento posizionato casualmente sullo schermo), la sua lunghezza aumenta.  
  L’aggiunta di un nuovo segmento avviene in testa al serpente, mantenendo la coerenza del movimento e della logica di gioco.

- **Collisioni:**  
  Il gioco termina se il serpente collide con i bordi dello schermo o con se stesso.  
  La collisione viene rilevata controllando se la posizione della testa coincide con quella di un segmento del corpo o con i limiti del campo di gioco.

- **Punteggio:**  
  Ogni volta che il serpente mangia il cibo, il punteggio aumenta.  
  Il punteggio viene visualizzato sullo schermo tramite la libreria SDL_ttf.

### Input dell’utente

L’utente controlla la direzione del serpente utilizzando i tasti freccia della tastiera.  
Gli input vengono gestiti tramite la libreria SDL, che intercetta gli eventi della tastiera e li trasmette al gioco.  
La direzione del serpente può essere cambiata solo se non è opposta alla direzione corrente, per evitare movimenti “impossibili”.


### Rendering grafico

Il rendering del gioco avviene tramite la libreria SDL, che si occupa di disegnare il serpente, il cibo e lo sfondo sullo schermo. La libreria SDL_ttf viene utilizzata per visualizzare il punteggio e altri messaggi di testo. Grazie alla compilazione con Emscripten, il rendering avviene all’interno di un canvas HTML, permettendo l’esecuzione del gioco direttamente nel browser.


## **Installazione e Avvio**

Spiega come compilare e avviare il progetto:

Il gioco Snake è stato pubblicato online e può essere giocato direttamente dal browser, senza necessità di installare o compilare nulla.

### Come giocare

1. **Apri il gioco** nel tuo browser all’indirizzo: https://moris99311.github.io/snake

2. **Usa i tasti freccia** (su, giù, sinistra, destra) per controllare il serpente.



### Requisiti

- **Browser moderno** (come Chrome, Firefox, Edge, Safari)
- **Connessione Internet** (solo per il primo caricamento)



### Per sviluppatori: compilazione e test locali

Se vuoi modificare il codice o testare localmente, puoi seguire questi passaggi:

1. **Installa Emscripten** seguendo le [istruzioni ufficiali](https://emscripten.org/docs/getting_started/downloads.html).
2. **Assicurati di avere SDL e SDL_ttf** compatibili con Emscripten.
3. **Compila il progetto** con:


## **Documentazione del Codice**


#### Funzioni Principali
1. **`Fill_cell()`**  
   Riempie una cella della griglia con un colore specificato.  
   *Implementazione:* Usa `SDL_FillRect` per disegnare un rettangolo nella posizione (x,y).

2. **`griglia()`**  
   Disegna la griglia di gioco.  
   *Scelta progettuale:* Linee sottili (1px) per mantenere la visibilità senza distrarre.

3. **`tail_snake()`**  
   Renderizza tutto il serpente iterando sulla lista collegata.  
   *Ottimizzazione:* Scorre la lista una sola volta per minimizzare le operazioni di rendering.

4. **`reset_apple()`**  
   Posiziona la mela in una cella libera.  
   *Algoritmo:* Genera posizioni casuali finché non trova una cella non occupata dal serpente.

5. **`lengthen_snake()`**  
   Aggiunge un nuovo segmento in testa al serpente.  
   *Logica:* Alloca un nuovo elemento e lo collega alla testa corrente.

6. **`remove_tail()`**  
   Rimuove l'ultimo segmento (coda).  
   *Gestione memoria:* Libera la memoria del segmento rimosso per prevenire memory leak.

7. **`check_wall_collision()`** & **`check_self_collision()`**  
   Rilevano collisioni con i bordi o con il corpo.  
   *Efficienza:* O(1) per i muri, O(n) per l'auto-collisione (scansione lista).

8. **`process_input()`**  
   Gestisce gli input da tastiera con SDL.  
   *Controllo:* Impedisce inversioni dirette (es. da destra a sinistra).

9. **`game_loop()`**  
   Cuore del gioco. Coordina:  
   - Input utente
   - Aggiornamento stato gioco
   - Rendering (serpente, mela, testo)
   - Gestione game over

#### Variabili Globali
- `psnake`: Puntatore alla testa del serpente (lista collegata)
- `direction`: Direzione corrente (struttura con dx, dy)
- `apple`: Posizione della mela
- `running`: Flag di stato gioco (1=attivo, 0=game over)
- `last_move`, `move_interval`: Controllo temporizzazione movimento

#### Scelte Implementative Chiave
1. **Rappresentazione Serpente**  
   Lista collegata con:
   - Aggiunta in testa durante il movimento
   - Rimozione dalla coda se non si mangia
   - Crescita per aggiunta diretta in testa quando si mangia

2. **Gestione Tempo**  
   Movimento controllato da `move_interval` (120ms) per garantire fluidità indipendente dalla velocità di rendering.

3. **Cross-Platform**  
   Uso di `#ifdef __EMSCRIPTEN__` per differenziare il loop principale tra browser e sistemi nativi.

---

### File HTML/JavaScript (Generati)

#### Integrazione Web
- **Canvas:** Emscripten genera automaticamente un elemento `<canvas>` dove viene renderizzato il gioco
- **Gestione Input:** Gli eventi tastiera sono gestiti direttamente da SDL tramite binding JavaScript
- **Asset:** Il font "Arial.ttf" viene caricato tramite filesystem virtuale di Emscripten
- **Entry Point:** Il loop principale è gestito da `emscripten_set_main_loop()` per ottimizzare l'esecuzione nel browser


## **Esempi di Uso**

Inserisci screenshot o GIF del gioco in azione.

## **Librerie e Dipendenze**

Ecco la descrizione delle librerie utilizzate nel progetto e le motivazioni alla base della loro scelta:



### **SDL (Simple DirectMedia Layer)**

- **Funzione:**  
  SDL è una libreria cross-platform che fornisce funzionalità di gestione di grafica, input e audio.
- **Motivazione:**  
  È stata scelta per la sua semplicità d’uso, la portabilità e la compatibilità con Emscripten. SDL permette di gestire facilmente la finestra, il rendering grafico e gli input da tastiera, rendendo il codice facilmente adattabile sia a sistemi desktop che web.
- **Utilizzo nel progetto:**  
  Viene utilizzata per creare la finestra di gioco, disegnare la griglia, il serpente e la mela, e per gestire gli eventi di input.

---

### **SDL_ttf**

- **Funzione:**  
  SDL_ttf è un’estensione di SDL che permette di renderizzare testo utilizzando font TrueType.
- **Motivazione:**  
  È stata scelta per visualizzare informazioni di gioco come il punteggio e il messaggio di game over direttamente sulla superficie di gioco, senza dover ricorrere a soluzioni esterne.
- **Utilizzo nel progetto:**  
  Viene utilizzata per visualizzare la lunghezza del serpente e il messaggio “GAME OVER” a schermo.

---

### **Emscripten**

- **Funzione:**  
  Emscripten è una toolchain che permette di compilare codice C/C++ in WebAssembly, rendendolo eseguibile nei browser moderni.
- **Motivazione:**  
  È stata scelta per portare il gioco Snake, scritto in C, direttamente sul web, senza dover riscrivere la logica di gioco in JavaScript. Emscripten offre un’integrazione trasparente con SDL e SDL_ttf, mantenendo la compatibilità con le librerie native.
- **Utilizzo nel progetto:**  
  Viene utilizzata per compilare il codice C in WebAssembly e generare i file HTML e JavaScript necessari per l’esecuzione nel browser.

---

### **WebAssembly**

- **Funzione:**  
  WebAssembly è un formato binario che permette l’esecuzione efficiente di codice nativo nei browser.
- **Motivazione:**  
  È stato scelto per garantire performance elevate e una buona compatibilità con i browser moderni.
- **Utilizzo nel progetto:**  
  Il codice C compilato con Emscripten viene eseguito come WebAssembly all’interno della pagina web.

---

### **HTML/JavaScript**

- **Funzione:**  
  HTML e JavaScript sono utilizzati per la pagina web che ospita il gioco e per integrare il codice WebAssembly.
- **Motivazione:**  
  Sono necessari per visualizzare il gioco nel browser e per gestire l’interazione tra l’utente e il codice compilato.
- **Utilizzo nel progetto:**  
  Il file HTML generato da Emscripten contiene il canvas su cui viene renderizzato il gioco, mentre il codice JavaScript si occupa dell’inizializzazione e della comunicazione con WebAssembly.

---

## **Problemi Noti e TODO**

### Bugs conosciuti

Al momento non sono stati riscontrati bug rilevanti nell’implementazione corrente del gioco.  
Il codice è stato testato su diversi browser e sistemi, garantendo una buona stabilità e un’esperienza utente fluida.



### Feature da implementare

Ecco alcune idee per migliorare e arricchire il gioco in futuro:

- **Tasto "Restart Game":**  
  Aggiungere un pulsante o una combinazione di tasti per riavviare la partita senza dover ricaricare la pagina.
- **Classifica dei punteggi:**  
  Implementare un sistema di salvataggio e visualizzazione dei migliori punteggi ottenuti, possibilmente persistente tra le sessioni di gioco.
- **Modalità di difficoltà:**  
  Introdurre diverse modalità di gioco che aumentano la difficoltà, ad esempio velocizzando il serpente, riducendo lo spazio di gioco o aggiungendo ostacoli.
- **Personalizzazione:**  
  Permettere all’utente di personalizzare alcuni aspetti del gioco, come il colore del serpente, della mela o dello sfondo.

---

## **Autore e Contatti**

* **Nome** Antonio Morace
* **Email** antonio.morace@icloud.com
* **GitHub** https://github.com/moris99311

## **Licenza**

Questo progetto è rilasciato sotto la licenza **MIT**.

### Cosa significa la licenza MIT?

La licenza MIT permette a chiunque di utilizzare, modificare, distribuire e vendere il software, sia per uso personale che commerciale, a condizione che venga inclusa la nota di copyright originale e la licenza in tutte le copie o parti sostanziali del software.

La licenza MIT non fornisce alcuna garanzia e non si assume alcuna responsabilità per eventuali danni derivanti dall’uso del software.

Per maggiori dettagli, consulta il file [LICENSE](LICENSE) incluso nel repository.
