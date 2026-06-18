# Codex Start

Diese Datei ist der Root-Einstieg für ChatGPT Codex.

Codex liest `AGENTS.md` automatisch als Projektanweisung. Diese Datei bleibt
deshalb bewusst der zentrale Codex-Einstieg im Root.

## Lies Zuerst

1. `index.md`
2. `DOKUMENTATION/Informationen/Start_und_Orientierung.md`
3. `VORLAGE/REGELN/GRUNDREGELN.md`
4. `VORLAGE/AI/PROJEKTREGELN/PROJEKTREGELN.md`
5. `VORLAGE/AI/AGENTEN/AGENTS.md`
6. `VORLAGE/AI/SKILLS/SKILL.md`
7. `DOKUMENTATION/SKILL.md`

## Codex-Arbeitsorte

- `PROJEKT/WORKSPACE/`: konkreter Projektinhalt.
- `PROJEKT/WORKSPACE/DOKUMENTATION/`: Dokumentation des konkreten Produkts.
- `DOKUMENTATION/`: Vorlagen- und Entwicklungsdokumentation.
- `VORLAGE/`: Regeln, Agenten, Skills und Tooling.
- `DEMOS/OPENROUTER/`: separater Demo- und Testbereich.

## Repo-Skills

Codex-sichtbare Skills liegen unter `.agents/skills/`.

Wichtig:

- Nutze `rg` für Suche.
- Verwende `git mv` für Strukturänderungen.
- Erzeuge keine zusätzlichen sichtbaren Root-Dateien ohne dokumentierten Grund.
- Für GitHub und Tool-Kompatibilität bleiben `README.md`, `LICENSE`,
  `CHANGELOG.md`, `VERSION`, `SECURITY.md`, `CLAUDE.md`, `claude.md`,
  `AGENTS.md` und `index.md` im Root erlaubt.
- Prüfe nach OpenRouter-Änderungen:

```bash
npm --prefix DEMOS/OPENROUTER run check
```

## Sicherheit

Keine Secrets, Tokens, Zahlungsdaten, personenbezogenen Daten oder
Sessiondaten ausgeben, speichern oder versionieren.

## 🔒 Lokal-only — Playtests, Backups & sensible Daten

Diese Daten dürfen **niemals** die lokale Maschine verlassen — weder nach GitHub noch nach Live/Deploy:

- **Playtests:** Play-Test-Branches (`PlayTest*`) und -Artefakte (`PlayTest/`, Protokolle, Screenshots) bleiben lokal.
- **Backups:** DB-Dumps, `*.sql`, `*.sql.gz`, `BACKUPS/` bleiben lokal — nie nach GitHub, nie in den Webroot/Live.
- **Sensible Daten:** `.env*` (außer `.env.example`), Tokens, API-Keys, Passwörter, `*.pem`, `*.key`, Zugangsdaten — niemals committen/pushen/deployen.
- **Push-Disziplin:** Nur den Hauptbranch (`main`) pushen, **niemals** `git push --all`/`--mirror`. `PlayTest*`-Branches werden nie gepusht.

Alle genannten Muster gehören in `.gitignore`. Technische Absicherung: der Pre-Push-Hook aus dem [DEV-Skill](https://github.com/MichaelGahnDESIGN/DEV-Skill) (`dev/hooks/pre-push`) blockiert solche Pushes hart — empfohlen, am besten global via `git config --global core.hooksPath ~/.git-hooks`.
