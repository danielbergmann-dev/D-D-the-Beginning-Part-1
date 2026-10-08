# Nebelpfad – Die letzte Laterne

Ein atmosphärisches, deutschsprachiges Solo-Rollenspiel für Handy und Tablet. **Teil I: Dornwacht** ist ein abgeschlossenes erstes Kapitel mit drei Enden und vorbereiteter Kontinuität für weitere Teile.

## Spielen

Statische Web-App: kein Konto, kein Server, keine API-Schlüssel, keine Laufzeit-Abhängigkeiten. Beweglicher Held auf vier gemalten Schauplätzen, Tippen-zum-Laufen mit Wegfindung, Würfelanimation, optionale Kämpfe, Tagebuch und automatische lokale Speicherung. Auf dem Startbildschirm installierbar und nach vollständigem Erstladen offline nutzbar.

### GitHub Pages

Unter **Settings → Pages → Build and deployment → Source: GitHub Actions** aktivieren. Danach den Workflow **Test and deploy adventure** starten (Actions → Run workflow), falls der erste Lauf mangels Pages-Einrichtung fehlschlägt.

Vorgesehene URL: https://danielbergmann-dev.github.io/D-D-the-Beginning-Part-1/

Diese URL ist erst nach einem erfolgreichen Pages-Deployment erreichbar. Der Workflow testet vor der Veröffentlichung und lädt ausschließlich öffentliche Spielfiles hoch, keine Spoiler-Dokumentation.

### Lokal starten

```sh
python3 -m http.server 4173
```

Im Browser http://localhost:4173 öffnen. Nicht per file:// öffnen, da JavaScript-Module und Service Worker einen Webserver benötigen.

## Steuerung

- Weg antippen: allein laufen.
- Markierten Ort antippen: hinlaufen und untersuchen.
- **Orte**: gleichwertige Alternative über große Buttons, auch für Tastaturbedienung.
- Pfeiltasten / WASD: Bewegung auf dem Desktop.
- Würfel: antippen, Ergebnis lesen, weiter.
- Kampf: rundenbasiert. Angriff, Vorbereitung/Deckung, Ausweichen, Heiltrank oder Rückzug.
- **Tagebuch**: Hinweise und letzte Würfe. **Held**: Werte, Gepäck und Regeln.
- **Menü → Spielstand sichern**: JSON-Export. Derselbe Export enthält das Vermächtnis für spätere Teile.

## Umfang und Regeln

Vier Schauplätze, drei Einsteigerprofile, mehrere Fertigkeitsproben, ein optionaler Wächterkampf, drei Ausgänge. Dies ist ein kompakter erster spielbarer Teil, keine große offene Welt. Die komplette SRD-Regelpalette ist bewusst nicht implementiert.

SRD-Regelkern: W20 + Modifikator gegen Schwierigkeit / Rüstung; Vorteil und Nachteil; Initiative; kritische Angriffstreffer; Schadenswürfel. Ausdrückliche Hausregeln: feste Profile, vereinfachte Bewegung und Rast, Vorbereitung in Deckung, Erholung nach Niederlage. Siehe [Regeln](docs/RULES.md).

## Projektstruktur

- `index.html`, `style.css`: responsive Oberfläche ohne Framework.
- `app.mjs`: UI, Würfel, Audio, Speichern/Import/Export.
- `engine.mjs`: Zustand und unabhängig testbare Spielregeln.
- `story.mjs`: Szenen, Bedingungen und Konsequenzen.
- `world.mjs`: Canvas-Rendering und kollisionsgeprüfte Wegfindung.
- `assets/worlds.webp`: erzeugte gemalte Hintergrundgrafik, vier Räume als Atlas.
- `docs/STORY-BIBLE.md`: **Spoiler**, Chronologie, Regeln der Welt und Fortsetzungsplanung.
- `docs/ASSETS.md`: Bildquelle und Erzeugungsprompt.
- `tests/engine.test.mjs`: automatisierte Regeln-, Routen- und Kontinuitätstests.

```sh
npm test
```

Keine Installation erforderlich; Node.js 22 oder neuer empfohlen. Bei Änderungen an ausgelieferten Dateien die Cache-Version in `sw.js` erhöhen.

## Speicherung und Datenschutz

Nur localStorage auf dem verwendeten Gerät. Keine Analyse, Werbung, Konten oder Netzwerkdienste. Browserdaten löschen entfernt den Spielstand. Export ist der geräteübergreifende Sicherungsweg. Ein laufender Kampf wird beim erneuten Laden als Rückzug behandelt; bisherige Lebenspunkte und verbrauchte Tränke bleiben erhalten. Würfel nutzen `crypto.getRandomValues` mit Rejection Sampling.

## Ausblick

Teil II führt nach Aschenhafen. Unterschiedliche Ausgangslagen des Endes, der Umgang mit dem Wächter, Runas Brief, der Erinnerungsverlust und Ivens Versorgung sind im Export enthalten. Teil II selbst ist noch nicht implementiert. Vor einer größeren Erweiterung sollten echte Touch-Tests auf iOS/Android, aufwendigere Charakteranimationen und taktische Bewegung im Kampf folgen.

## Urheber und Regelgrundlage

Eigene Welt, Geschichte und Darstellung. Nicht von Wizards of the Coast unterstützt oder genehmigt. SRD-Attribution siehe [NOTICE.md](NOTICE.md). Weitere Rechte am selbst erstellten Projekt bleiben beim Rechteinhaber; es wird hier keine allgemeine Open-Source-Lizenz für das Gesamtprojekt erklärt.
