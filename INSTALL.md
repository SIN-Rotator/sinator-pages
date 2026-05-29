# SINator Pages — Installation

*Public Landing Page für den SINator Fireworks AI Key Pool. Reines Static HTML — kein Build, keine Dependencies.*

---

## 1. Voraussetzungen

Dieses Projekt ist eine **einzige statische HTML-Datei**. Es gibt keine Build-Tools, kein Node.js, kein Python (außer für den lokalen Server).

```bash
# Nur zum Servieren lokal:
which python3
# ✅ "/opt/homebrew/bin/python3" oder "/usr/bin/python3"
# ❌ Python wird nur für den HTTP-Server gebraucht — geht auch mit `npx serve`
```

Für Produktion:
- **Cloudflare Pages** Konto (verbunden mit GitHub `SIN-Rotator/sinator-pages`)

---

## 2. Repository klonen

```bash
cd ~/dev
git clone git@github.com:SIN-Rotator/sinator-pages.git
cd sinator-pages

# ✅ Das gesamte Projekt = 1 Datei: index.html
ls -la
# index.html
```

---

## 3. Lokal servieren (Entwicklung)

**Option A — Python (built-in, kein Install):**

```bash
python3 -m http.server 8000
# → http://localhost:8000

# ✅ "Serving HTTP on :: port 8000"
# Öffne http://localhost:8000 im Browser
```

**Option B — Node.js `serve` (falls Node installiert):**

```bash
npx serve .
# → http://localhost:3000
```

---

## 4. Änderungen testen

```bash
# 1. index.html bearbeiten
# 2. Browser refreshen (F5 / Cmd+R)
# ✅ Änderungen sind sofort sichtbar — kein Build-Schritt
```

Das JS in der Seite ruft die SINator Backend-API auf:
```javascript
// Aktuell konfigurierte Backend-URL:
const API_BASE = "https://sinator.delqhi.com";
// Für lokale Entwicklung auf localhost ändern:
// const API_BASE = "http://localhost:8000";
```

**Wenn lokal getestet wird:** `API_BASE` auf `http://localhost:8000` setzen und `SINator-fireworksai` Backend starten.

---

## 5. Deployment (Cloudflare Pages)

```bash
# Push to main — Cloudflare Pages deployed automatisch:
git add index.html
git commit -m "..."
git push origin main
# ✅ Cloudflare Pages: "Build successful" — Seite live in ~30s
```

**Cloudflare Pages Config (im Dashboard):**
| Setting | Wert |
|---------|------|
| Build command | *(leer — kein Build)* |
| Output directory | `/` (Repo-Root) |
| Framework | None |

---

## 6. Verifikation

```bash
# Lokal:
curl http://localhost:8000
# ✅ Gibt HTML zurück (enthält "SINator" im Title)

# Produktion:
curl https://sinator-pages.pages.dev
# ✅ Gibt dieselbe HTML-Seite zurück
```

---

## 7. Fehlerbehebung

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Leere Seite im Browser | Falscher Pfad | `python3 -m http.server` im Repo-Root ausführen |
| API Calls schlagen fehl | `API_BASE` zeigt auf Produktion | Auf `http://localhost:8000` ändern (Schritt 4) |
| CORS Error | Backend blockiert lokale Anfragen | `SINATOR_AUTH_TOKEN` setzen oder CORS-Origins erweitern |
| Cloudflare Deploy fehlschlägt | Build-Fehler | Cloudflare Pages verwendet kein Build — Output-Dir muss `/` sein |

---

*Stand: 2026-05-29 | Static HTML | Cloudflare Pages*
