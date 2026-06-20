# 🌍 GEO Quiz – 1. Jahrgang (GWB)

Ein interaktives Quiz zur Wiederholung des Geografie-Stoffs der 1. Klasse, basierend auf dem Skript **„1. Klasse GEO“**. Die Klimawandel-Themen sind bewusst ausgenommen.

Die App ist eine **einzelne HTML-Datei** – kein Build, keine Installation, keine externen Abhängigkeiten. Läuft in jedem Browser und direkt über GitHub Pages.

## ✨ Funktionen

- **Namenseingabe** vor dem Start
- **Online-Rangliste** über alle Geräte hinweg – 1 Punkt je richtiger Antwort
- **Monatlicher Reset** – die Rangliste zeigt automatisch nur den aktuellen Monat
- **Themenauswahl** – einzelne Themenbereiche an-/abwählen oder alles zusammen üben
- **Gemischte Fragen** – Multiple Choice **und** Eingabefragen (Lückentext)
- **Sofortiges Feedback** mit kurzer Erklärung zu jeder Frage
- **Fragen mischen** und optionale **Schnellrunde** (15 Fragen)
- **Auswertung** mit Prozentwert und Ergebnis pro Themenbereich
- Tolerante Eingabeprüfung (Groß-/Kleinschreibung und Umlaute egal)

> Ohne Einrichtung läuft die Rangliste sofort, aber **nur lokal auf dem jeweiligen Gerät**.
> Für eine **gemeinsame Rangliste über alle Schüler-Geräte** einmalig Supabase einrichten (siehe unten).

## 📚 Enthaltene Themen

1. Grundlagen der Geografie (Sphären, Erdrotation/-revolution, Jahreszeiten)
2. Karten & Orientierung (Maßstab, Kartenarten, Gradnetz, GPS)
3. Plattentektonik (Krustenarten, Plattengrenzen, Konvektionsströme)
4. Vulkane & Erdbeben (Vulkantypen, Richterskala, seismische Wellen, Tambora)
5. Gebirge & Kräfte (endogen/exogen, Verwitterung, Erosion, Gletscher)
6. Klimazonen & Vegetation
7. Ökosystem Wüste (Aridität, Desertifikation)
8. Weltbevölkerung (Verteilung, Megastädte, Push-/Pull-Faktoren)
9. Migration (Arten, freiwillig/unfreiwillig, Push-/Pull-Faktoren, Brain Drain)
10. Entwicklung & Einkommensstufen (Factfulness / Gapminder)

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

## 🏆 Gemeinsame Online-Rangliste einrichten (Supabase, kostenlos)

Damit alle Schüler:innen – egal auf welchem Gerät – in **derselben** Rangliste landen, brauchst du einen kleinen kostenlosen Datenspeicher. Wir nutzen **Supabase** (kein Server, keine Kreditkarte, dauerhaft kostenloser Tarif). Einmal eingerichtet, ca. 10 Minuten:

### 1. Konto + Projekt anlegen
1. Auf [supabase.com](https://supabase.com) registrieren (z. B. mit GitHub-Login).
2. **New project** anlegen: Namen vergeben (z. B. `geo-quiz`), ein Datenbank-Passwort setzen (kannst du dir notieren, wird hier nicht weiter gebraucht), Region **Central EU** wählen → **Create new project**. Kurz warten, bis das Projekt bereit ist.

### 2. Tabelle für die Punkte erstellen
1. Links im Menü auf **SQL Editor** → **New query**.
2. Folgenden Code einfügen und auf **Run** klicken:

```sql
create table scores (
  id bigint generated always as identity primary key,
  name text not null,
  points int not null,
  month_key text not null,
  created_at timestamptz default now()
);

alter table scores enable row level security;

create policy "jeder darf eintragen" on scores
  for insert to anon with check (true);

create policy "jeder darf lesen" on scores
  for select to anon using (true);
```

Das legt die Tabelle an und erlaubt dem Quiz, Punkte einzutragen und die Rangliste zu lesen.

### 3. Zugangsdaten kopieren
1. Links unten auf **Project Settings** (Zahnrad) → **API**.
2. Kopiere dir zwei Werte:
   - **Project URL** (z. B. `https://abcdxyz.supabase.co`)
   - **anon public** key (langer Text, beginnt mit `eyJ…`)

> Der `anon`-Key darf öffentlich sein – durch die Regeln oben kann man damit nur Punkte eintragen und die Rangliste lesen, sonst nichts.

### 4. Werte in die App eintragen
Öffne `index.html`, suche oben im `<script>` den Abschnitt **KONFIGURATION RANGLISTE** und ersetze die zwei Platzhalter:

```js
const SUPABASE_URL = "https://abcdxyz.supabase.co";   // deine Project URL
const SUPABASE_KEY = "eyJhbGciOiJI...DEIN_LANGER_KEY"; // dein anon public key
```

Speichern, die geänderte `index.html` wieder zu GitHub hochladen – fertig. Ab jetzt sehen alle dieselbe Rangliste.

### Monatlicher Reset
Passiert **automatisch**: Jeder Eintrag bekommt einen Monats-Schlüssel (z. B. `2026-06`), und die Rangliste zeigt immer nur den laufenden Monat. Am Monatsersten startet die Liste von selbst leer – alte Einträge bleiben in der Datenbank erhalten, falls du sie nachsehen willst (Supabase → **Table Editor → scores**).

> Falls du die Werte **nicht** einträgst, funktioniert alles trotzdem – die Rangliste wird dann nur lokal pro Gerät gespeichert (gut zum Testen oder für einen einzelnen Klassen-PC).

## ✏️ Fragen ändern oder ergänzen

Alle Fragen stehen im `<script>`-Block in `index.html` in der Liste `QUESTIONS`.

- `type:"mc"` → Multiple Choice: `options:[...]`, `answer:` = Index der richtigen Antwort (beginnend bei 0)
- `type:"text"` → Eingabe: `accept:[...]` = Liste akzeptierter Antworten
- `fb:` = Erklärung, die nach dem Beantworten angezeigt wird

Neue Frage einfach nach demselben Muster ergänzen – das passende Thema erscheint automatisch in der Auswahl.

---

*Lernhilfe für den Unterricht. Inhalte zusammengefasst aus dem Schulskript.*
