# Esercitazione - Analisi della sopravvivenza dei siti archeologici nel tempo

Per scaricare questa guida in formato PDF cliccare su [questo link](https://kdrive.infomaniak.com/app/share/408009/f1ddaaef-a24a-4681-bdcb-5184f3f22f8b).

L’obiettivo di questo esercizio è di registrare se un sito sia sopravvissuto o meno dagli anni '70 fino ad oggi, utilizzando immagini satellitari CORONA e una mappa di base moderna. Questo documento elencherà i passaggi da eseguire in successione, fornendo suggerimenti dove necessario.

Scaricare i dati a [questo link](https://kdrive.infomaniak.com/app/share/408009/49395dcf-a149-44fc-9f12-1d0ebff11846).

Aprire il progetto vuoto "patrimonio_culturale.qgz" e connettersi al geopackage "cultural_heritage" che si trova nella cartella "gpk" all'interno della cartella del progetto.
Una volta connessi al geopackage, caricare i layer "siti_archeo", "fiumi", e "laghi".

> [!Hint] Suggerimento
> Per connettersi ad un database geopackage, andare sul pannello Browser, cliccare con il tasto destro su Geopackage e selezionare "Nuova Connessione".

![[null]]

Caricare una mappa di base per poter visualizzare il territorio. Utilizzare il plugin QuickMapService (Web -> QuickMapServices) per caricare una mappa a scelta tra **Google Satellite** e **Bing Satellite**.

![[CleanShot 2022-05-25 at 15.41.47.png]]

Caricare anche tutte le immagini satellitari CORONA, contenute nella cartella **``raster``** del progetto. 

> [!warning] Attenzione
> Una volta caricate, è consigliato, specialmente su computer meno recenti, di attivare un'immagine alla volta, altrimenti l'intera sessione di QGIS  potrebbe rallentare.
> 

## Creare un luogo dove registrare la visibilità dei siti da satellite

Obiettivo: creare un nuovo campo all'interno della tabella attributi del layer siti_archeo in cui registrare la visibilità dei siti da satellite.

Aprire la tabella attributi del layer siti_archeo ![[CleanShot 2022-05-25 at 18.44.38.png]] e aggiungere un nuovo campo testuale. Scegliere un nome del campo a piacimento (ad es. "visibilità"). In questo campo verrà registrato se un sito è visibile solo sulle immagini CORONA, solo sulle immagini moderne, o su entrambe.

> [!tip] Suggerimento
>  Per aggiungere un nuovo campo attivare prima le modifiche del layer ![[CleanShot 2022-05-25 at 14.41.29.png]] e poi cliccare sul pulsante apposito nella tabella attributi ![[CleanShot 2022-05-25 at 18.47.59.png]]. 
>  Nella schermata di aggiunta campo, ricordare di scegliere il tipo Testo ![[CleanShot 2022-05-25 at 18.48.59.png]] 
>  Nel geopackage la lunghezza del campo può essere lasciata a 0)

## Verificare la visibilità dei siti nelle diverse immagini satellitari

**Obiettivo**: registrare se un sito è visibile solamente sulle CORONA, solamente sulle immagini moderne (Google o Bing, a seconda di quello che si è scelto in precedenza), oppure su entrambe.

Per ogni sito, zoomare sulla posizione di un sito ed accendere e spegnere l'immagine CORONA lasciando attiva la mappa di base Google o Bing in background. Scrivere poi "corona", "moderne", od "entrambe" nel campo "visibilità" del layer siti_archeo a seconda del risultato dell'analisi visiva.
Ricordarsi di salvare spesso il progetto. ![[CleanShot 2022-05-25 at 14.47.13.png]]

> [!tip] Suggerimento
> Per scrivere nel campo creato, ricordarsi di "accendere" le modifiche del layer ![[CleanShot 2022-05-25 at 14.41.29.png]]
> Per facilitare lo spostamento nella mappa ed evitare di ritornare sullo stesso sito per errore, selezionare il sito nella tabella attributi (cliccando sul numero della riga a sinistra) e cliccando poi su "Zoom mappa alle righe selezionate" in alto ![[CleanShot 2022-05-25 at 19.03.14.png]]

## Visualizzare il risultato dell'analisi

**Obiettivo**: creare una simbologia categorizzata basata sul campo relativo alla visibilità dei siti.

Andare nel pannello di simbologia del layer e cambiare la simbologia in categorizzato (![[CleanShot 2022-05-25 at 19.08.53.png]]), scegliendo come valore nel menu a tendina il campo che si è creato in precedenza (ad es. visibilità).

Aggiustare i colori dei simboli a piacimento.

> [!tip] Suggerimento
> Ricordarsi di cliccare su "Classifica" una volta selezionato il campo, altrimenti non verrà visualizzato nulla.
> Per modificare i colori, fare doppio click sul simbolo nella lista delle varie categorie.

![[CleanShot 2022-05-25 at 19.12.16.png]]

Ricordarsi di riorganizzare l'ordine dei layer nel caso fossero posti in un ordine non corretto (ad es. siti sotto i laghi ecc.).

## Creare una mappa

**Obiettivo**: esportare una mappa con la visibilità della categorizzazione appena effettuata.

La mappa dovrà contenere i seguenti elementi:
- Mappa con i layer **``siti_archeo``**, **``laghi``**, e **``fiumi``**
	- Rimuovere le immagini CORONA
	- La mappa di base (Bing o Google) può essere lasciata o tolta.
- Barra di scala
- Freccia del nord
- Legenda

Alcuni comandi utili da ricordare per la creazione della mappa sono:
- Creare un nuovo layout di stampa  ![[CleanShot 2022-05-25 at 16.01.38.png]]

Nel layout di stampa:
- Selezionare un oggetto ![[CleanShot 2022-05-25 at 19.33.06.png]]
- Spostare il contenuto dell'oggetto ![[CleanShot 2022-05-25 at 19.33.46 1.png]] (utile per muovere e zoomare la mappa dal layout di stampa)
- Zoom completo ![[CleanShot 2022-05-25 at 19.34.47.png]] (utile nel caso ci si muova inavvertitamente con lo zoom)
- Inserire la mappa nel foglio  ![[CleanShot 2022-05-25 at 14.58.48.png]]
- Inserire barra di scala  ![[CleanShot 2022-05-25 at 14.59.06.png]]
- Inserire il nord  ![[CleanShot 2022-05-25 at 14.59.21.png]]
- Inserire legenda  ![[CleanShot 2022-05-25 at 14.59.41.png]]
	- Per un miglior risultato, spuntare la casella "aggiorna automaticamente" e rinominare "visibilità" come "Visibilità dei siti archeologici" e spuntare anche la casella "Cornice" per fornire una cornice alla legenda.
	- ![[CleanShot 2022-05-25 at 19.30.48.png]]
	- Esportare immagine  ![[CleanShot 2022-05-25 at 16.18.15.png]]