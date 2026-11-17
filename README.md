# KartX

Statistiche locali per **Mario Kart Wii / Retro Rewind** su Windows.

Questa repository contiene **solo i file di distribuzione** di KartX: installer,
checksum, informazioni sulla versione e changelog. Il codice sorgente non è pubblico e
non è presente qui.

## Download

Apri la pagina [Releases](../../releases/latest) e scarica l'ultimo installer:

```
KartX-Setup-<versione>.exe
```

Le versioni precedenti restano disponibili nella stessa pagina.

## Installazione

1. Scarica l'installer della versione desiderata.
2. Eseguilo: l'installazione è **per-utente**, non richiede privilegi di amministratore
   e non installa servizi.
3. Avvia KartX dal menu Start (o dal collegamento sul desktop, se selezionato).

KartX si installa in `%LOCALAPPDATA%\Programs\KartX`. I dati delle gare restano in
`%APPDATA%\KartX` e non vengono rimossi dalla disinstallazione.

## Requisiti

- Windows 10 1809 o successivo, 64 bit (Windows 11 supportato).
- WebView2 Evergreen per l'interfaccia integrata. È presente su Windows 11 e sulla
  maggior parte dei Windows 10; se manca, KartX apre l'interfaccia nel browser predefinito.
- Il gioco avviato per registrare le gare.

## Verifica del download

Ogni release include un file `.sha256`. Su PowerShell:

```powershell
Get-FileHash .\KartX-Setup-<versione>.exe -Algorithm SHA256
```

Il valore deve coincidere con quello pubblicato nelle note della release.

## Aggiornamento

Esegui l'installer della nuova versione: sostituisce i file dell'applicazione e conserva
i dati locali. Non è necessario disinstallare la versione precedente.

## Disinstallazione

Impostazioni di Windows → App → KartX → Disinstalla. La cartella `%APPDATA%\KartX`
(database e log) resta sul computer: rimuovila manualmente solo se vuoi cancellare anche
lo storico delle gare.

## Changelog

Le modifiche di ogni versione sono nella pagina Releases e nel file
[CHANGELOG.md](CHANGELOG.md).

## Sicurezza e privacy

KartX legge la memoria del gioco in sola lettura, non richiede account e non invia dati a
servizi online. Le statistiche restano sul computer dell'utente.

L'installer non è firmato digitalmente: Windows SmartScreen può mostrare un avviso al
primo avvio. Verifica sempre il checksum pubblicato.
