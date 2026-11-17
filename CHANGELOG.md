# Changelog

Modifiche visibili a chi usa KartX. Il formato segue [Keep a Changelog](https://keepachangelog.com/it/1.1.0/)
e le versioni seguono [Semantic Versioning](https://semver.org/lang/it/).

La pipeline di release estrae da qui la sezione corrispondente al tag: **la sezione
deve esistere e non essere vuota prima di creare il tag**. Le note devono restare
adatte al pubblico: niente percorsi interni, dettagli di implementazione sensibili,
credenziali o informazioni su infrastruttura privata.

## [Unreleased]

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
