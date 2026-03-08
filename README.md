# n8n Launcher – iPhone Web App

Mobile-optimierte PWA zum Starten deiner n8n-Workflows per Knopfdruck.

## Features

- **Skripte starten** – Tippe auf "Starten" um den n8n-Webhook aufzurufen
- **Status anzeigen** – Läuft / Fertig / Fehler direkt auf der Karte
- **Alle starten** – Alle Skripte nacheinander ausführen
- **Protokoll** – Verlauf aller Ausführungen mit Zeitstempel
- **Offline-Speicherung** – Konfiguration bleibt im Browser gespeichert
- **iPhone Home Screen** – Als App installierbar (Add to Home Screen)

## Setup

### 1. Icons generieren

Öffne `generate-icon.html` im Browser – die Icons werden automatisch heruntergeladen.
Lege `icon-192.png` und `icon-512.png` in denselben Ordner wie `index.html`.

### 2. Auf GitHub Pages hosten

```bash
git init
git add .
git commit -m "n8n launcher"
gh repo create n8n-launcher --public --push --source=.
# dann in GitHub Repo > Settings > Pages > Branch: main, Root
```

Danach erreichbar unter: `https://DEINUSER.github.io/n8n-launcher/`

### 3. n8n Webhook konfigurieren

In n8n:
- Workflow mit **Webhook-Trigger** erstellen
- Trigger-Einstellung: **"Respond when last node finishes"** → App wartet auf Fertigstellung
- Webhook-URL kopieren (z.B. `http://192.168.1.100:5678/webhook/mein-workflow`)

### 4. Skript in der App hinzufügen

- Auf **＋** tippen
- Name, Beschreibung, Webhook-URL eingeben
- Methode: POST (empfohlen) oder GET
- Icon wählen → Speichern

### 5. Als iPhone-App installieren

1. App-URL in Safari öffnen
2. Teilen-Symbol → **"Zum Home-Bildschirm"**
3. Fertig – startet wie eine native App

## n8n Webhook-Einstellung für Status-Anzeige

Damit die App sieht, wann ein Skript fertig ist, muss in n8n der Webhook auf
**"Respond when last node finishes"** gestellt sein:

```
Webhook Node → Settings → "Respond" → "When last node finishes"
```

Dann wartet der Fetch-Aufruf bis das Workflow beendet ist.

## Einstellungen

- **Timeout**: Wie lange (Sekunden) auf Antwort gewartet wird (Standard: 30s)
- **Bearer Token**: Für n8n-Webhooks mit Header-Auth
- **Export/Import**: Backup deiner Skript-Konfiguration als JSON
