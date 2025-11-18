# Wort-Zuordnungsspiel für Deno Deploy

Ein Multiplayer WebSocket-Spiel, bei dem Spieler Worte eingeben und diese dann den Spielern zuordnen müssen.

## Projektstruktur

```
.
├── server.ts           # Hauptserver (WebSocket + Static Files)
├── public/
│   └── index.html     # Frontend (HTML, CSS, JavaScript)
└── deno.json          # Deno Konfiguration
```

## Lokale Entwicklung

```bash
deno run --allow-net --allow-read server.ts
```

Oder mit deno task:
```bash
deno task dev
```

Öffne dann http://localhost:8000

## Deployment auf Deno Deploy

1. **GitHub Repository erstellen:**
   - Pushe diesen Code zu GitHub

2. **Deno Deploy Projekt erstellen:**
   - Gehe zu https://dash.deno.com/new
   - Wähle dein GitHub Repository
   - **Entry Point:** `server.ts`
   - Klicke auf "Deploy"

3. **Custom Domain verbinden:**
   - Gehe zu deinem Projekt in Deno Deploy
   - Klicke auf "Settings" → "Domains"
   - Füge deine Domain hinzu (z.B. `josualucas.com`)
   - Folge den DNS-Anweisungen

## Was wurde gegenüber der ursprünglichen Version geändert?

### Server (server.ts):
- ❌ **Entfernt:** `const PORT = 8080` (Deno Deploy hat keine festen Ports)
- ❌ **Entfernt:** `Deno.serve({ port: PORT }, handler)`
- ✅ **Hinzugefügt:** Routing für statische Dateien (HTML)
- ✅ **Geändert:** WebSocket läuft auf `/ws` statt Root
- ✅ **Geändert:** `Deno.serve(handler)` ohne Port-Parameter
- ✅ **Hinzugefügt:** TypeScript-Typen für bessere Typsicherheit

### Frontend (index.html):
- ✅ **Geändert:** WebSocket-URL nutzt jetzt `window.location.host` statt `localhost:8080`
- ✅ **Geändert:** WebSocket-Pfad ist jetzt `/ws`
- ✅ **Geändert:** Automatische Protokoll-Erkennung (ws:// oder wss://)

### Neue Dateien:
- ✅ **Erstellt:** `deno.json` für Task-Konfiguration
- ✅ **Erstellt:** `public/` Ordner für statische Dateien

## Features

- ✅ Multiplayer WebSocket-Verbindungen
- ✅ Lobby-System mit 6-stelligen Codes
- ✅ Echtzeit-Synchronisation
- ✅ Drag & Drop Interface
- ✅ Mobile-freundlich (Touch-Support)
- ✅ Automatische SSL (wss://) bei HTTPS

## Technologie-Stack

- **Backend:** Deno mit WebSockets
- **Frontend:** Vanilla JavaScript (kein Framework nötig!)
- **Hosting:** Deno Deploy (serverless)
- **Keine Datenbank nötig** (alles im Speicher)
