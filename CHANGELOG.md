# Changelog

Modifiche visibili a chi usa KartX. Il formato segue [Keep a Changelog](https://keepachangelog.com/it/1.1.0/)
e le versioni seguono [Semantic Versioning](https://semver.org/lang/it/).

La pipeline di release estrae da qui la sezione corrispondente al tag: **la sezione
deve esistere e non essere vuota prima di creare il tag**. Le note devono restare
adatte al pubblico: niente percorsi interni, dettagli di implementazione sensibili,
credenziali o informazioni su infrastruttura privata.

## [0.2.1] - 2026-11-20

Questa release aggiunge la presence Discord, le sessioni reali di gara e la vista Lista
delle piste, e corregge la conclusione delle gare e la griglia Tracks.

### Aggiunto

- **Discord Rich Presence** opzionale: mostra in Discord l'attività di KartX (in attesa del
  gioco, lobby, gara con pista/posizione/giro, gara terminata) tramite il protocollo RPC
  locale di Discord. Richiede un Application ID configurato in Settings; l'immagine
  opzionale si imposta con la chiave dell'asset caricato nel Developer Portal. Nessun
  nickname o dato privato viene condiviso.
- **Sessioni reali** nel database: un Grand Prix finito e una sessione online continua sono
  entità distinte. La pagina Grand Prix permette di aprire una sessione e vedere le gare
  che contiene; lo storico precedente resta separato come ricostruzione.
- **Vista Lista** nella sezione Tracks, con toggle Griglia/Lista e preferenza salvata in
  locale; entrambe le viste usano gli stessi dati, filtri e ordinamento.
- **Penultimo arrivato**: la gara viene finalizzata quando il penultimo partecipante
  taglia il traguardo, senza attendere l'ultimo kart.

### Corretto

- La griglia Tracks non mostra più virgole tra le card: il rendering unisce esplicitamente
  le card invece di interpolare un array in una stringa.
- Le gare concluse normalmente non vengono più marcate come interrotte quando l'ultimo
  giocatore non arriva o quando lo stage risultati arriva insieme a `active=false`.
- Le sessioni rimaste aperte dopo un crash/chiusura vengono chiuse all'avvio senza
  spostare o riclassificare le gare.

### Note tecniche

- Schema SQLite v5 additivo (`race_sessions`, `races.session_id`); le gare storiche non
  ricevono un `session_id` inventato. Il database esistente viene aggiornato al primo
  avvio senza perdere le gare già registrate.
- Il numero di gare di un GP privato non è esposto dal runtime: le lobby private restano
  sessioni online e non vengono spezzate a 4/8 gare.

### Problemi noti

- L'installer non è firmato digitalmente: Windows SmartScreen può chiedere una conferma
  al primo avvio.
- La presence Discord richiede un Application ID configurato; l'immagine è opzionale e
  deve corrispondere a un asset caricato nel Developer Portal.

## [0.2.0] - 2026-11-17

### Aggiunto

- Traiettorie reali a 10 Hz per tutti i partecipanti, con colori distinti, selezione dei
  piloti e dei giri, zoom, tooltip e playback sincronizzato sul tempo di gara.
- Mappa condivisa per pista costruita come mediana dei giri realmente percorsi, con
  interruzioni sui salti di telemetria e bounds limitati al corridoio guidato.
- Installer Windows per-utente (Inno Setup), con versione allineata al tag e checksum
  SHA-256.
- Release automatiche: un tag `vX.Y.Z` compila, esegue i test e pubblica installer,
  checksum, `version.json` e note nella repository pubblica `KartX-Releases`.

### Migliorato

- La versione mostrata nell'applicazione deriva dai metadati dell'eseguibile e non da un
  valore duplicato nell'interfaccia.
- I campionamenti ad alta velocità non vengono più spezzati in frammenti: la soglia di
  salto tiene conto delle velocità reali del gioco.

### Corretto

- La mappa non usa più il giro più lento come riferimento: prima poteva includere
  testacoda e uscite di pista e deformare l'intera visualizzazione.
- Le escursioni fuori pista non allargano più i bounds della mappa.

### Note tecniche

- Richiede Windows 10 1809 o successivo, 64 bit.
- L'installer è per-utente (`%LOCALAPPDATA%\Programs\KartX`), non richiede privilegi di
  amministratore e conserva i dati in `%APPDATA%\KartX` durante gli aggiornamenti.

### Problemi noti

- L'installer non è firmato digitalmente: Windows SmartScreen può chiedere una conferma
  al primo avvio.
- La proiezione delle traiettorie è 2D: ponti, gallerie e sezioni sovrapposte possono
  apparire sovrapposti; la quota è disponibile nei tooltip.
- Non è ancora presente un aggiornamento automatico integrato.

## [0.1.0] - 2026-11-17

- Prima release pubblica: acquisizione locale della telemetria, salvataggio SQLite,
  dashboard, Race History, Tracks, Rivals, Statistics, Grand Prix e impostazioni.
