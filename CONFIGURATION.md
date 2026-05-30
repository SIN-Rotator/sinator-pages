# SINator Pages — Konfiguration

---

## 1. API-Backend URL

**Datei:** `index.html`

```javascript
// Produktion (Cloudflare Pages):
const API_BASE = "https://sinator.delqhi.com";

// Lokale Entwicklung:
// const API_BASE = "http://localhost:8000";
```

Bei lokaler Entwicklung `API_BASE` auf `http://localhost:8000` setzen.

---

## 2. Deployment (Cloudflare Pages)

**Auto-Deploy:** Jeder `git push origin main` deployed automatisch.

**Cloudflare Pages Config (im Dashboard):**
| Setting | Wert |
|---------|------|
| Build command | *(leer — kein Build)* |
| Output directory | `/` (Repo-Root) |
| Framework | None |

**Custom Domain:** `sinator.delqhi.com` (CNAME auf Cloudflare Pages)

---

## 3. Keine weiteren Konfigurationen

Dieses Projekt ist eine **einzige statische HTML-Datei** ohne Build-Tools, Dependencies oder Server-Konfiguration.

---

*Stand: 2026-05-30 | Static HTML | Cloudflare Pages*
