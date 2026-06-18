# DEPLOY — Vorlage

Generisches Runbook für den Release-Workflow (`/dev`). Diese Datei ist eine
**Vorlage**. In einer neuen Projektkopie werden Hosting, Domain, Account, Datenbank
und Pfade durch die echten projektspezifischen Werte ersetzt.

> Zugangsdaten gehören **niemals** ins Repository, sondern in eine lokale,
> gitignorierte Zugangsdaten-Datei bzw. eine `.env` außerhalb des Web-Roots.

## Voraussetzungen
- Zugangsdaten liegen lokal und gitignoriert (FTP/MySQL/SSH) — nie im Repo.
- SSH-/FTP-Zugang zum Zielserver ist eingerichtet.
- Datenbank-Schema ggf. einmalig eingespielt.
- Server-Konfiguration (`config.php` o. Ä.) liegt außerhalb des Repos.

## Preflight
Projektspezifischen Build-/Syntax-Check eintragen, z. B.:
```
find PROJEKT/WORKSPACE -name "*.php" | head -5
```

## Build
Projektspezifischen Build-Schritt eintragen (oder „kein Build" vermerken).

## Tests
Vorhandene Tests ausführen bzw. manuelle Smoke-Tests beschreiben.

## Deploy
Deploy-Weg projektspezifisch beschreiben (Beispiel mit Platzhaltern):
```
lftp <FTP_HOST> -u <FTP_USER>,<FTP_PASSWORT> -e "
  mirror -R PROJEKT/WORKSPACE/ <ZIEL_WEBROOT>/;
  chmod -R 755 <ZIEL_WEBROOT>/;
  bye"
```

## Verify
Nach dem Deploy Smoke-Tests gegen die echte Domain durchführen
(HTTP-Statuscodes, Login-Flow, API-Antworten).

## WICHTIG
- Secrets nie committen (Zugangsdaten-Datei, `**/config.php`, Migrationsskripte).
- Bei FTP ggf. Dateirechte nach jedem Mirror setzen (`chmod -R 755`).
