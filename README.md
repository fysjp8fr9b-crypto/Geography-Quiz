# 🌍 GEO Quiz – 1. Jahrgang (GWB)

Ein interaktives Quiz zur Wiederholung des Geografie-Stoffs der 1. Klasse, basierend auf dem Skript **„1. Klasse GEO“**. Die Klimawandel-Themen sind bewusst ausgenommen.

Die App ist eine **einzelne HTML-Datei** – kein Build, keine Installation, keine externen Abhängigkeiten. Läuft in jedem Browser und direkt über GitHub Pages.

## ✨ Funktionen

- **Themenauswahl** – einzelne Themenbereiche an-/abwählen oder alles zusammen üben
- **Gemischte Fragen** – Multiple Choice **und** Eingabefragen (Lückentext)
- **Sofortiges Feedback** mit kurzer Erklärung zu jeder Frage
- **Fragen mischen** und optionale **Schnellrunde** (15 Fragen)
- **Auswertung** mit Prozentwert und Ergebnis pro Themenbereich
- Tolerante Eingabeprüfung (Groß-/Kleinschreibung und Umlaute egal)

## 📚 Enthaltene Themen

1. Grundlagen der Geografie (Sphären, Erdrotation/-revolution, Jahreszeiten)
2. Karten & Orientierung (Maßstab, Kartenarten, Gradnetz, GPS)
3. Plattentektonik (Krustenarten, Plattengrenzen, Konvektionsströme)
4. Vulkane & Erdbeben (Vulkantypen, Richterskala, seismische Wellen, Tambora)
5. Gebirge & Kräfte (endogen/exogen, Verwitterung, Erosion, Gletscher)
6. Klimazonen & Vegetation
7. Ökosystem Wüste (Aridität, Desertifikation)
8. Weltbevölkerung (Verteilung, Megastädte, Push-/Pull-Faktoren)
9. Entwicklung & Einkommensstufen (Factfulness / Gapminder)

## 🚀 Lokal starten

Einfach die Datei `index.html` im Browser öffnen – fertig.

## 🌐 Auf GitHub Pages veröffentlichen

1. Neues Repository auf GitHub anlegen (z. B. `geo-quiz`).
2. Die Dateien `index.html` und `README.md` hochladen (oder per Git pushen).
3. Im Repository auf **Settings → Pages** gehen.
4. Unter **Build and deployment → Source** „**Deploy from a branch**“ wählen.
5. Branch **`main`** und Ordner **`/ (root)`** auswählen, **Save** klicken.
6. Nach kurzer Zeit ist das Quiz erreichbar unter:
   `https://<dein-benutzername>.github.io/geo-quiz/`

### Per Git hochladen (optional)

```bash
git init
git add index.html README.md
git commit -m "GEO Quiz – erste Version"
git branch -M main
git remote add origin https://github.com/<dein-benutzername>/geo-quiz.git
git push -u origin main
```

## ✏️ Fragen ändern oder ergänzen

Alle Fragen stehen im `<script>`-Block in `index.html` in der Liste `QUESTIONS`.

- `type:"mc"` → Multiple Choice: `options:[...]`, `answer:` = Index der richtigen Antwort (beginnend bei 0)
- `type:"text"` → Eingabe: `accept:[...]` = Liste akzeptierter Antworten
- `fb:` = Erklärung, die nach dem Beantworten angezeigt wird

Neue Frage einfach nach demselben Muster ergänzen – das passende Thema erscheint automatisch in der Auswahl.

---

*Lernhilfe für den Unterricht. Inhalte zusammengefasst aus dem Schulskript.*
