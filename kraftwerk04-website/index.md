# Kraftwerk 04 – Website

Statische Website des Fitnessstudios **Kraftwerk 04** (TuS Huchting von 1904 e. V.) in Bremen-Huchting.

Die Seite ist ein **fertig gebautes statisches Bundle** (HTML + CSS-in-JS + JavaScript, alle Bilder lokal). Es gibt **keinen Build-Step und kein `npm install`** – die Dateien können direkt ausgeliefert werden.

## Lokal starten

Kein Setup nötig. Eine der folgenden Varianten:

```bash
# Variante 1: Node (ohne Installation, lädt "serve" on-the-fly)
npx serve .

# Variante 2: Python (auf den meisten Systemen vorinstalliert)
python3 -m http.server 8080
```

Oder in VS Code: Extension **Live Server** → Rechtsklick auf `index.html` → „Open with Live Server".

Danach im Browser öffnen: `http://localhost:8080` (Port je nach Variante).

> Hinweis: Die Seite per Doppelklick auf `index.html` (file://) öffnen funktioniert **nicht** zuverlässig – bitte immer über einen lokalen Server.

## Deployment auf Vercel

1. Dieses Repo zu GitHub pushen:
   ```bash
   git init
   git add .
   git commit -m "Kraftwerk 04 Website – statischer Export"
   git branch -M main
   git remote add origin https://github.com/yacobhanstomas/kraftwerk04-website.git
   git push -u origin main
   ```
2. Auf [vercel.com](https://vercel.com) → **Add New → Project** → das GitHub-Repo importieren.
3. Einstellungen:
   - **Framework Preset:** `Other`
   - **Build Command:** *(leer lassen)*
   - **Output Directory:** `./`
   - **Install Command:** *(leer lassen)*
4. **Deploy** – fertig. Jeder weitere Push auf `main` deployed automatisch.

## Nach dem Deployment: Domain eintragen

Aktuell steht als Platzhalter-Domain `https://kraftwerk04-website.vercel.app` in drei Dateien. Nach dem ersten Deploy (oder beim Verbinden einer eigenen Domain) bitte ersetzen:

- `index.html` → `canonical`, `og:url`, `og:image`
- `robots.txt` → `Sitemap:`-Zeile
- `sitemap.xml` → `<loc>`

## Projektstruktur

```
kraftwerk04-website/
├── index.html            # Einzige Seite (One-Pager mit Anker-Navigation)
├── js/
│   └── bundle.js         # Kompiliertes App-Bundle (React, fertig gebaut)
├── assets/
│   └── images/           # Alle Bilder lokal (hero, strength, cardio, …)
├── favicon.svg           # Favicon (modern, SVG)
├── favicon.ico           # Favicon (Fallback, 16/32/48 px)
├── apple-touch-icon.png  # iOS-Icon (180×180)
├── robots.txt
├── sitemap.xml
├── .gitignore
└── README.md
```

> Abweichung vom ursprünglichen Plan: `robots.txt`, `sitemap.xml` und die Favicons liegen im **Root** statt in `public/` – ohne Build-Step wird das Repo-Root 1:1 ausgeliefert, und diese Dateien müssen unter `/robots.txt` bzw. `/favicon.ico` erreichbar sein.

## Technische Hinweise

- **Kein Backend, keine Datenbank, keine Secrets.** Die Seite ist ein reiner One-Pager.
- **Kontakt:** erfolgt über `tel:`- und `mailto:`-Links sowie Google-Maps-Route. Es gibt bewusst kein Kontaktformular. Falls später eines gewünscht ist, empfiehlt sich ein externer Form-Service wie [Formspree](https://formspree.io) (HTML-Formular mit `action="https://formspree.io/f/…"` – kein eigenes Backend nötig).
- **Google Fonts** (Bebas Neue, Manrope) werden bewusst extern per `<link>` eingebunden.
- **Google Maps** wird als iframe eingebunden (Karte + Routenplaner-Links).
- **Bilder:** stammen von Unsplash und wurden lokalisiert (`assets/images/`). Unsplash-Lizenz: kostenlose Nutzung ohne Namensnennung erlaubt.
- **Große Dateien:** aktuell ist das größte Asset ~340 KB – Git LFS ist **nicht** nötig. Falls später Videos o. ä. > 25 MB dazukommen: [Git LFS](https://git-lfs.com) einrichten, bevor sie committet werden.
- **Impressum & Datenschutz:** sind als Dialoge im Footer der Seite integriert (kein separater Server nötig).

## Inhalt pflegen

Texte, Öffnungszeiten, Bewertungen und Bilder stehen im kompilierten Bundle. Für inhaltliche Änderungen am besten im ursprünglichen Emergent-Projekt ändern und den Export erneut durchführen – oder die Änderung direkt in `js/bundle.js` vornehmen (das Bundle ist lesbar, nicht minifiziert; Texte lassen sich per Suche finden, z. B. `Öffnungszeiten`, `Montag`, `IMAGES`).
