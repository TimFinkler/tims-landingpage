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
  tim-cutout.webp   freigestelltes Porträt für den Hero-Bereich
  tim-portrait.jpg  Originalfoto, dient als Vorschaubild beim Teilen (og:image)
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

## Das freigestellte Porträt

`tim-cutout.webp` ist das Hero-Bild ohne Hintergrund: per Segmentierungsmodell
(U²-Net, Variante für Personen) aus dem Originalfoto gelöst, Kante um rund einen
Pixel eingezogen, damit kein heller Saum bleibt, und unten weich ausgeblendet –
dadurch taucht das Motiv aus dem Dunkel auf, statt abgeschnitten zu wirken.
Schatten und Lichtkranz entstehen in CSS über `drop-shadow` und folgen deshalb
automatisch der Silhouette.

Für ein neues Foto: freistellen (jedes Werkzeug, das transparentes PNG/WebP
ausgibt), unten ausblenden, als WebP mit Transparenz speichern und die Datei
ersetzen. Die Maße im `<img>` (`width`/`height`) anpassen, sonst springt das
Layout beim Laden.

Das Hero-Bild wird **nur als WebP** ausgeliefert. Alle Browser ab etwa 2020
können das; wer ältere unterstützen muss, legt zusätzlich ein PNG daneben und
baut ein `<picture>`-Element darum.

## Inhalte ändern

Alles steht direkt in `index.html`. Die Farben, Schriften und Abstände sind oben im `<style>` als Custom Properties im `:root`-Block definiert – dort ändern, und es greift auf der ganzen Seite.

| Variable | Bedeutung |
| --- | --- |
| `--accent` / `--accent-ink` | Kupfer, der Akzentton |
| `--teal` / `--teal-ink` | Petrol, der zweite Ton |
| `--ink`, `--muted` | Text |
| `--bg`, `--surface`, `--line` | Flächen und Linien |

Die Startseite ist bewusst **nur dunkel** – die Lichtstimmung trägt das Design. Impressum und Datenschutz folgen dagegen der Systemeinstellung.

## Bewegung

Alles Animierte sitzt im `<script>` ganz unten und respektiert `prefers-reduced-motion`:

| Element | Was passiert |
| --- | --- |
| Intro | Porträt, Chips, Headline und Buttons kommen gestaffelt herein |
| Lichter (`.orb`) | driften langsam im Hintergrund |
| Zeiger | weicher Lichtschein folgt der Maus, Porträt bewegt sich leicht mit |
| Karten | Schimmer folgt dem Zeiger über die Karte |
| Buttons `.magnetic` | ziehen den Zeiger leicht an |
| Zeitstrahl | die Linie im Werdegang füllt sich beim Scrollen |
| Abschnitte `.reveal` | blenden beim Scrollen ein (Sicherheitsnetz: nach 2,5 s sind sie in jedem Fall sichtbar) |
| Fortschrittsbalken | oben am Rand, zeigt die Scroll-Position |

Wer es ruhiger mag: Im Markup die Klasse `reveal` entfernen, oder im `<style>` den Block unter `@media (prefers-reduced-motion: no-preference)` löschen.
