# Esercitazione - Analisi Diacronica della posizione dei siti archeologici sul territorio

Per scaricare questa guida in formato PDF cliccare su [questo link](https://kdrive.infomaniak.com/app/share/408009/3fba9021-7e8e-4b3a-baf8-4064be75600d).

L’obiettivo di questo esercizio è di mappare la disposizione dei siti sul territorio durante diversi periodi storici, utilizzando una simbologia tramite regole del layer. Questo documento elencherà i passaggi da eseguire in successione, fornendo suggerimenti dove necessario.

Scaricare i dati a [questo link](https://kdrive.infomaniak.com/app/share/408009/fb6a4e99-d30d-4e76-ad1d-78b6d4c56c52).

Aprire il progetto vuoto "analisi_diacronica.qgz" e caricare lo shapefile siti_archeo, contenuto nella cartella shp all'interno della cartella del progetto.

> [!warning] Attenzione
> Ricordarsi di caricare il file corretto, ovvero quello che termina con .shp oppure senza un'estensione finale. In Windows è possibile verificare che il file sia uno shapefile dalla colonna "Tipo di File".

Caricare poi il file siti_archeo_dati.csv dalla cartella "csv" del progetto. Questo file contiene le informazioni sull'occupazione temporale dei siti archeologici.

> [!tip] Suggerimento
> È sempre possibile trascinare direttamente lo shapefile nel progetto, senza caricarlo per forza tramite il gestore sorgente dati ![[CleanShot 2022-05-25 at 15.39.10.png]]. La stessa cosa si può fare per il csv, visto che questo contiene solo informazioni qualitative e non relative alle coordinate dei siti.


Caricare una mappa di base per poter visualizzare il territorio. Utilizzare il plugin QuickMapService (Web -> QuickMapServices) per caricare una mappa a scelta tra **Google Satellite** e **Bing Satellite**.

![[CleanShot 2022-05-25 at 15.41.47.png]]

> [!warning] Attenzione
> 
Assicurarsi che il layer e il progetto condividano lo stesso sistema di riferimento (```EPSG: 32637```), altrimenti alcune funzioni più avanti potrebbero non funzionare. Per verificarlo, controllare il valore epsg in basso a destra del progetto (![[CleanShot 2022-05-25 at 15.40.24 1.png]]) e poi quello del layer spostando il mouse sul layer stesso e aspettando che appaia un pop-up informativo.

![[CleanShot 2022-05-25 at 15.49.41.png]]


## Unire le informazioni spaziali con quelle tabellari

**Obiettivo**: unire la tabella siti_archeo_dati con il layer "siti_archeo" ed esportare il risultato.

Eseguire un join tabellare tra il layer siti_archeo e il layer tabellare siti_archeo_dati tramite il pannello **Join**  ![[CleanShot 2022-05-25 at 15.57.08.png]] presente nelle proprietà del layer (doppio-click sul layer o tasto destro-> Proprietà)

Nel pannello di join aggiungere una nuova unione ![[CleanShot 2022-05-25 at 15.55.45.png]] ed eseguire il join utilizzando come **Vettore di join** il layer siti_archeo_dati. Come **Campo unione** e **Campo destinazione** scegliere "site_name".
Selezionare poi i campi da unire e sceglere "**EBA**", "**MBA**", "**LBA**", "**IA**", "**site_type**", rinominare anche il nome del campo unito per togliere qualsiasi prefisso.

![[CleanShot 2022-05-25 at 16.02.46.png]]

> [!tip] Suggerimento
>  Ricordarsi di cliccare su "Applica" prima di cliccare su Ok e chiudere la finestra delle proprietà del layer, giusto per essere sicuri che tutto venga applicato correttamente.

Esportare il risultato in un nuovo geopackage tramite tasto destro su layer -> Esporta -> Salva elementi come. Chiamare il geopackage analisi_diacronica e salvare il layer con un nome a scelta, come ad es. "siti_archeo_occupazione".

> [!attention] Attenzione
> Nel menu di esportazione del layer, al campo Nome File, ricordarsi di usare il menu ![[CleanShot 2022-05-25 at 16.11.52 1.png]] per indicare la posizione dove si vuole salvare il geopackage e di non inserire semplicemente un nome, altrimenti l'esportazione fallirà.

Ricordarsi di salvare spesso il progetto. ![[CleanShot 2022-05-25 at 14.47.13.png]]

## Simbologia tramite regole

**Obiettivo**: impostare una simbologia tramite regole che permetta di visualizzare i diversi periodi di occupazione dei siti con diverse simbologie.

Nel layer appena salvato, caricare lo stile **```stile_periodo_tipo```** presente nella cartella del progetto.

> [!tip] Suggerimento
>  Per caricare uno stile da file, aprire la finestra delle proprietà del layer e andare alla scheda "Simbologia", cliccare su Stile in basso -> Carica stile e selezionare il file dal menu del campo File ![[CleanShot 2022-05-25 at 16.11.52 1.png]]

Completare la simbologia tramite regole già presente nel layer aggiungendone altre due tramite il ![[CleanShot 2022-05-25 at 16.23.19.png]] in basso nel pannello della simbologia del layer.
Le simbologie da aggiungere sono:
- Siti dell'età del Ferro (IA = 1.000000000000000)
- Siti dell'età del Ferro e di tipo 'tell'

Ricordarsi di fornire un'etichetta alle singole simbologie, in quanto è l'etichetta che poi apparirà nella mappa finale.

Per creare una nuova regola, utilizzare ![[CleanShot 2022-05-25 at 16.32.07.png]] e nel nuovo pannello che si aprirà utilizzare i dati e i comandi in **Campi e Valori** per selezionare il campo e i valori di interesse.
Ad es. ``` "EBA" = '1.000000000000000'```. 

> [!tip] Suggerimento
>  Si possono usare le regole già presenti per gli altri periodi, cambiando i valori dove necessario, ad esempio sostituendo 'MBA' con 'IA' e 'flat site' con 'tell'.

Una volta finito, è possibile, sempre dal pannello della simbologia del layer, attivare o disattivare una simbologia, così da vedere un solo periodo alla volta.

**OPZIONALE**: Fornire un simbolo differente alla simbologia dei tell rispetto a quella dei flat_sites, cambiando il simbolo da un punto ad es. ad un triangolo o simili (Doppio click sulla regola, poi cambiare il simbolo semplice)

![[CleanShot 2022-05-25 at 16.47.30.png]]

## Creare mappe di fase

**Obiettivo**: Creare mappe di fase e una mappa tipologica.

Le mappe da creare sono:
- Mappa con i siti EBA
- Mappa con i siti MBA
- Mappa con i siti LBA
- Mappa con i siti IA
- Mappa con i siti IA Flat sites e Tell

Ogni mappa dovrà contenere i seguenti elementi:
- Mappa con il layer siti_archeo_occupazione (o il nome scelto in precedenza)
	- Rimuovere eventuali altri layer come lo shapefile originale e il csv.
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
	- Per un miglior risultato, spuntare la casella "aggiorna automaticamente" e rinominare "siti_archeo_occupazione" come "Siti Archeologici" e spuntare anche la casella "Cornice" per fornire una cornice alla legenda.
	- ![[CleanShot 2022-05-25 at 16.41.102.png]]
-  Esportare immagine  ![[CleanShot 2022-05-25 at 16.18.15.png]]

> [!tip] Suggerimento
>  Per creare una serie di mappe in successione senza dover inserire nuovamente ogni cosa, senza chiudere il layout di stampa, ritornare nella schermata principale di qgis, e spuntare la casella di un'altra regola nella simbologia (ad es. togliendo la spunta ad EBA e mettendola ad MBA), ritornare nel layout di stampa e cliccare sul pulsante di aggiornamento della mappa ![[CleanShot 2022-05-25 at 16.43.49.png]] mantenendo tutti gli altri elementi come sono.

