# Esercitazione - analisi geoarcheologica del paesaggio
L’obiettivo di questo esercizio è di quantificare il numero di siti su unità geomorfologiche e produrre una mappa sulla quale saranno  rappresentati entrambi, utilizzando una mappa geomorfologica e digitalizzando i singoli elementi lì rappresentati. Questo documento elencherà i passaggi da eseguire in successione, fornendo suggerimenti dove necessario.

Aprire il progetto vuoto "analisi paesaggio.qgz" e connettersi al geopackage "landscape" che si trova nella cartella "gpk" all'interno della cartella del progetto.
Una volta connessi al geopackage, caricare il layer "sweyhat_sites".

> [!Hint] Suggerimento
> Per connettersi ad un database geopackage, andare sul pannello Browser, cliccare con il tasto destro su Geopackage e selezionare "Nuova Connessione".

![[CleanShot 2022-05-25 at 14.02.53.png]]



> [!warning] Attenzione
> 
Assicurarsi che il layer e il progetto condividano lo stesso sistema di riferimento (```EPSG: 32637```), altrimenti alcune funzioni più avanti potrebbero non funzionare. Per verificarlo, controllare il valore epsg in basso a destra del progetto (![[CleanShot 2022-05-25 at 15.40.24 1.png]]) e poi quello del layer spostando il mouse sul layer stesso e aspettando che appaia un pop-up informativo.

![[CleanShot 2022-05-25 at 14.33.18 4.png]]

**Opzionale** - Caricare una mappa di base per poter visualizzare meglio il territorio. Utilizzare il plugin QuickMapService (Web -> QuickMapServices) per caricare una mappa a scelta.


## Georeferire la mappa geomorfologica

**Obiettivo**:  georeferire la mappa geomorfologica così da utilizzarla in GIS. 

Procedere alla georeferenziazione della mappa geomorfologica. Aprire il georeferenziatore raster (Menu Raster -> Georeferenziatore), e caricare l'immagine ![[CleanShot 2022-05-25 at 15.33.32.png]]  contenuta nella cartella raster del progetto -> "wilk_sweyhat.png". 

Caricare il file con i ground control points utili per georeferire l'immagine ![[CleanShot 2022-05-25 at 14.36.36.png]].

Nelle impostazioni ![[CleanShot 2022-05-25 at 14.35.16.png]] modificare il **Tipo di trasformazione** in **Polinomiale 3** e assicurarsi che l'**SR di destinazione** sia lo stesso di quello del progetto (32637). 

**Opzionale** - aggiungere un altro paio di punti GCP (non necessario)
> [!Hint] Suggerimento
> È possibile utilizzare i siti archeologici come punti gcp, confrontando i nomi dei siti nel layer siti_archeo con i nomi segnati sulla mappa.

Una volta selezionati eventuali nuovi GCP e impostato la trasformazione, è possibile lanciare la georeferenziazione  ![[CleanShot 2022-05-25 at 14.27.15.png]]

> [!warning] Info
> È normale che l'immagine appaia molto distorta e quasi "ripiegata" ai lati dove non erano presenti GCP, questo è dovuto al tipo di trasformazione, necessaria per assicurarci che le parti della mappa che ci interessano si posizionino correttamente.

Il risultato finale dovrebbe essere simile a questo:

![[CleanShot 2022-05-25 at 14.39.59.png]]

## Digitalizzare la mappa geomorfologica

**Obiettivo**: Creare poligoni per tutte le unità geomorfologiche rappresentate nella mappa.

Caricare il layer poligonale "geomorf" dal geopackage "landscape". 
Come visibile, molti degli elementi geomorfologici sono già digitalizzati, l'obiettivo è quello di completare la digitalizzazione delle rimanenti unità geomorfologiche, in particolare:

- Main alluvial floodplain (type b/c)
- Ancient floodplain residual (type d)
- Euphrates river terraces
- Gully-eroded terrain
- Tributary wadis and their deposits


**Opzionale** Per distinguere meglio i singoli elementi, nel pannello Stile Layer è possibile cambiare la simbologia in "Categorizzata", scegliendo come Valore "geomorf_type" e poi cliccando su Classifica.
![[CleanShot 2022-05-25 at 14.50.55.png]]

Il layer geomorf è strutturato in modo da permettere di scegliere da un menu a tendina il tipo di unità geomorfologiche una volta che si sarà conclusa la digitalizzazione di un poligono.

> [!tip] Suggerimento
> Per digitalizzare, ricordarsi di "accendere" le modifiche del layer ![[CleanShot 2022-05-25 at 14.41.29.png]] e di creare un nuovo poligono ![[CleanShot 2022-05-25 at 14.41.50.png]]

Per un miglior risultato e per evitare buchi o poligoni sovrapposti, attivare anche gli strumenti d'aggancio ![[CleanShot 2022-05-25 at 14.43.02.png]]. Attivare sia l'aggancio al vertice  che al segmento e muoversi a vari livelli di zoom per una migliore digitalizzazione.
![[CleanShot 2022-05-25 at 14.43.42 1.png]]

Per evitare di agganciarsi ai siti archeologici, attivare l'opzione di aggancio solo al layer attivo.
![[CleanShot 2022-05-25 at 14.44.31.png]]

Una volta completata la digitalizzazione, chiudere le modifiche del layer (sempre dall'icona a matita) e salvare il progetto ![[CleanShot 2022-05-25 at 14.47.13.png]]. 
Caricare poi un nuovo stile da file, scegliendo il file stile_geomorfologia presente nella cartella del progetto. Salvare poi il layer come predefinito nel database della sorgente dati.

> [!tip] Suggerimento
>  Per caricare uno stile da file, aprire la finestra delle proprietà del layer e andare alla scheda "Simbologia", cliccare su Stile in basso -> Carica stile e selezionare il file dal menu del campo File ![[CleanShot 2022-05-25 at 16.11.52 1.png]]

## Calcolare il numero di siti su unità geomorfologica

**Obiettivo**:  calcolare il numero di siti che si trovano su ciascuna unità geomorfologica. 

Procedere a comprendere il numero di siti per unità geomorfologica.
Utilizzare l'algoritmo "Conta i punti nel poligono" .
![[CleanShot 2022-05-25 at 14.52.53.png]]

Nel campo poligoni scegliere il layer geomorf e nel campo punti scegliere il layer sweyhat_sites, lasciare poi tutti gli altri valori di default e cliccare su "Esegui" per lanciare l'algoritmo.

Il risultato verrà salvato in un layer temporaneo. Salvare quindi il layer "Numero" appena creato nel geopackage landscape con un nome a scelta.
> [!tip] Suggerimento
>  Quando si salva in un layer geopackage, ricordarsi di selezionare il tipo di file nel dialogo di esportazione e inserire il nome del nostro nuovo layer (qgis inserirà di default il nome del geopackage)

Ricordarsi di salvare spesso il progetto. ![[CleanShot 2022-05-25 at 14.47.13.png]]

**Opzionale**: esportare il risultato in un foglio excel (formato xlsx).

## Creare una mappa

**Obiettivo**:  creare una mappa con le unità geomorfologiche e i siti archeologici tramite il layout di stampa. 

La mappa dovrà contenere i seguenti elementi:
- Mappa con i layer **```geomorf```** e **```sweyhat_sites```**
	- Rimuovere eventuali altri layer come la mappa di base.
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
	- Per un miglior risultato, spuntare la casella "aggiorna automaticamente" e rinominare "sweyhat_sites" come "Siti Archeologici" e spuntare anche la casella "Cornice" per fornire una cornice alla legenda.
	- ![[CleanShot 2022-05-25 at 15.03.02.png]]
	- Esportare immagine  ![[CleanShot 2022-05-25 at 16.18.15.png]]