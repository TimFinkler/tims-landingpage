# tims-landingpage

Statische One-Page-Website für Tim Finkler – GenAI Entwickler & Berater, Köln.
Kein Build-Schritt, kein Framework: HTML, CSS und ein paar Zeilen JavaScript.

## Dateien

```
index.html          Startseite (CSS und JS inline)
impressum.html      Impressum – Platzhalter müssen vor dem Livegang ausgefüllt werden
datenschutz.html    Datenschutzerklärung – ebenso
favicon.svg         Monogramm TF
assets/img/         Fotos (optimiert, EXIF-Daten entfernt)
```

## Lokal ansehen

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Veröffentlichen

Jeder Static-Hoster funktioniert – Repository verbinden, Root-Verzeichnis als Quelle, fertig:

- **GitHub Pages**: Settings → Pages → Branch wählen → Root
- **Netlify / Vercel / Cloudflare Pages**: Repository importieren, kein Build-Command, Publish-Verzeichnis `/`
- Eigene Domain anschließend beim Hoster im DNS hinterlegen

## Vor dem Livegang erledigen

1. **Impressum und Datenschutz ausfüllen.** In beiden Dateien stehen Platzhalter in eckigen Klammern (Anschrift, Hosting-Anbieter, Löschfrist). Für ein Impressum ist in Deutschland eine ladungsfähige Anschrift vorgeschrieben.
2. **Entscheiden, ob die Telefonnummer öffentlich stehen soll.** Sie steht in `index.html` im Abschnitt `#kontakt` und in beiden Rechtsseiten.
3. **Optional: Google Fonts lokal einbinden.** Dann werden keine IP-Adressen an Google übertragen und der Abschnitt „Schriftarten" in der Datenschutzerklärung entfällt. Dazu die Schriften Archivo, IBM Plex Sans und IBM Plex Mono herunterladen, unter `assets/fonts/` ablegen, per `@font-face` einbinden und den `<link>` auf fonts.googleapis.com entfernen.
4. **Optional: LinkedIn / GitHub verlinken**, im Kontaktblock in `index.html`.

## Inhalte ändern

Alles steht direkt in `index.html`. Die Farben, Schriften und Abstände sind oben im `<style>` als Custom Properties im `:root`-Block definiert – dort ändern, und es greift auf der ganzen Seite.

| Variable | Bedeutung |
| --- | --- |
| `--accent` / `--accent-ink` | Kupfer, der Akzentton |
| `--teal` / `--teal-ink` | Petrol, der zweite Ton |
| `--ink`, `--muted` | Text |
| `--bg`, `--surface`, `--line` | Flächen und Linien |

Der Dark Mode ist in zwei Blöcken direkt darunter definiert (einmal `prefers-color-scheme`, einmal `[data-theme="dark"]`). Wer eine Farbe ändert, ändert sie in beiden.
