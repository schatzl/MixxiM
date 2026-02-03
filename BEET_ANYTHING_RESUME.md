# BEET ANYTHING - Entwickler-Resume

## 🎯 Schnellstart

**Produktname**: Beet Anything  
**Datei**: `gartenplaner-deutsch.html`  
**Typ**: Single-Page-Application (vollständig in einer HTML-Datei)  
**Sprache**: Vollständig Deutsch  
**Status**: Production Ready v1.0

---

## 📦 Was ist implementiert

### Kern-Features
✅ Mehrjahresplanung mit Historie  
✅ Dynamische Beetverwaltung  
✅ 20 deutsche Gemüsesorten mit Mischkultur-Daten  
✅ Intelligenter Vorschlagsalgorithmus (Scoring-basiert)  
✅ Kompatibilitäts-Matrix  
✅ Export/Import (JSON)  
✅ LocalStorage-Persistierung  
✅ Responsive Design (Desktop + Mobile)

### Technologie
- Pure JavaScript (ES6+, keine Frameworks)
- CSS Grid + Flexbox
- Google Fonts (Playfair Display, Merriweather)
- LocalStorage API
- File API (Import/Export)

---

## 🏗️ Architektur-Überblick

### Klassen (OOP-Hierarchie)

```
Gemuese              → Gemüsedaten + Begleiter-Logik
Gartenbeet           → Beet-Metadaten
Pflanzung            → Beet-Jahr-Gemüse-Verknüpfung
GartenManager        → Zentrale Datenverwaltung
VorschlagsEngine     → Algorithmus für optimale Zuweisung
```

### Datenfluss

```
User Input
    ↓
app.* Funktionen (Controller)
    ↓
GartenManager (Model)
    ↓
app.rendern() (View)
    ↓
DOM Update
```

### Wichtigste App-Methoden

```javascript
app.init()                          // Initialisierung, lädt Daten
app.jahrAendern(±1)                // Jahr navigieren
app.vorschlaegeGenerieren()        // Algorithmus starten
app.beetModalOeffnen(beetId)       // Beet bearbeiten
app.datenExportieren()             // JSON Download
app.datenImportieren()             // JSON Upload
app.matrixAnzeigen()               // Mischkultur-Matrix
app.speichern()                    // → LocalStorage
```

---

## 🧮 Algorithmus-Kernlogik

**Datei-Position**: `VorschlagsEngine.pflanzungsOptionBewerten()`

### Scoring-Gewichte:

| Kriterium | Punkte | Bedingung |
|-----------|--------|-----------|
| Familie-Rotation | +30 | Andere Familie als Vorjahr |
| Familie-Rotation | -20 | Gleiche Familie wie Vorjahr |
| Nährstoff-Rotation | +25 | Schwachzehrer nach Starkzehrer |
| Nährstoff-Rotation | -15 | Starkzehrer nach Starkzehrer |
| Guter Begleiter | +15 | Pro kompatible Pflanze |
| Schlechter Begleiter | -30 | Pro inkompatible Pflanze |
| Leeres Beet | +5 | Keine aktuellen Pflanzen |
| 2-Jahres-Rotation | -10 | Gleiche Pflanze vor 2 Jahren |

**Output**: Sortierte Liste mit Beet-Gemüse-Zuweisungen + Begründungen

---

## 📊 Datenstruktur

### LocalStorage Key
```javascript
'gartenplanerDaten'  // JSON-String
```

### JSON-Schema
```json
{
  "gemueseSorten": [
    {
      "id": "tomate",
      "name": "Tomate", 
      "naehrstoffbedarf": "hoch",
      "familie": "Nachtschattengewächse",
      "guteBegleiter": ["basilikum", "karotte"],
      "schlechteBegleiter": ["kartoffel", "kohl"]
    }
  ],
  "beete": [
    { "id": 1704636800000, "name": "Beet 1" }
  ],
  "pflanzungen": [
    { "beetId": 1704636800000, "jahr": 2024, "gemueseId": "tomate" }
  ]
}
```

---

## 🎨 Design-System

### CSS-Variablen
```css
--boden-dunkel: #3a2f28    /* Primärtext */
--blatt-gruen: #4a7c59     /* Primärfarbe */
--salbei: #8ba888          /* Sekundärfarbe */
--creme: #f4f1ea           /* Hintergrund */
--terrakotta: #c1694f      /* Akzent */
--sonnen-gelb: #e8b84d     /* Highlight */
```

### Nährstoff-Badges
```css
.naehrstoff-hoch    → Terrakotta
.naehrstoff-mittel  → Sonnengelb  
.naehrstoff-niedrig → Salbei
```

---

## 🔧 Häufige Anpassungen

### 1. Neue Gemüsesorte hinzufügen

**Position**: `GartenManager.gemueseDatenbankInitialisieren()`

```javascript
// Schritt 1: Gemüse erstellen
new Gemuese('mangold', 'Mangold', 'mittel', 'Fuchsschwanzgewächse')

// Schritt 2: Zu Liste hinzufügen
gemueseListe.push(neuesGemuese);

// Schritt 3: Begleiter festlegen
this.begleiterFestlegen('mangold',
    ['zwiebel', 'kohl'],      // Gute Begleiter
    ['spinat', 'rote-beete']  // Schlechte Begleiter
);
```

### 2. Scoring-Gewichte ändern

**Position**: `VorschlagsEngine.pflanzungsOptionBewerten()`

```javascript
// Beispiel: Familie-Rotation höher bewerten
bewertung += 50;  // statt 30
```

### 3. Neue Bewertungskriterien

```javascript
// Beispiel: Sonnenbedarf
if (gem.sonnenbedarf === 'voll' && beetLage === 'süden') {
    bewertung += 20;
    gruende.push('Optimale Sonneneinstrahlung');
}
```

### 4. UI-Text ändern

Suche nach String in HTML und ersetze:
```javascript
// Beispiel
"Gartenplan vorschlagen" → "Plan erstellen"
```

---

## 🐛 Debugging-Tipps

### LocalStorage prüfen
```javascript
// Browser-Konsole:
localStorage.getItem('gartenplanerDaten')
```

### Daten zurücksetzen
```javascript
// Browser-Konsole:
localStorage.removeItem('gartenplanerDaten')
location.reload()
```

### Algorithmus-Output testen
```javascript
// In Browser-Konsole:
app.vorschlagsEngine.pflanzungsOptionBewerten(beetId, 'tomate', 2024)
```

### Datenintegrität prüfen
```javascript
app.garten.pflanzungen.length          // Anzahl Pflanzungen
app.garten.beete.size                  // Anzahl Beete
app.garten.gemueseSorten.size          // Anzahl Gemüse (sollte 20 sein)
```

---

## 🚀 Nächste Entwicklungsschritte

### Priorität 1 (Quick Wins)
- [ ] Mehr Gemüsesorten (Ziel: 30-40)
- [ ] Aussaat/Ernte-Kalender
- [ ] Druckfunktion für Jahresplan

### Priorität 2 (Medium)
- [ ] Beetgrößen-Eingabe
- [ ] Flächenberechnung
- [ ] Pflanzabstände
- [ ] Notizfeld pro Beet

### Priorität 3 (Advanced)
- [ ] Grafische Beetvisualisierung (SVG/Canvas)
- [ ] Drag & Drop zwischen Beeten
- [ ] Benutzer-definierte Mischkultur-Regeln
- [ ] Mobile App (PWA)

---

## 📝 Code-Konventionen

### Namensgebung (Deutsch)
```javascript
// Variablen: camelCase
aktuellesJahr, wunschliste, beetId

// Klassen: PascalCase
Gemuese, Gartenbeet, VorschlagsEngine

// Methoden: camelCase + Verb
beetHinzufuegen(), vorschlaegeGenerieren()

// CSS-Klassen: kebab-case
.beet-kopf, .pflanze-zuweisung, .naehrstoff-badge
```

### Kommentare
```javascript
// Deutsch für Business-Logik
// Englisch für technische Details (optional)
```

---

## 🔍 Wichtige Dateipositionen

### Gemüse-Datenbank
**Zeile ~250-280**: `gemueseDatenbankInitialisieren()`

### Mischkultur-Regeln
**Zeile ~280-320**: `begleiterFestlegen()` Aufrufe

### Scoring-Algorithmus
**Zeile ~550-650**: `pflanzungsOptionBewerten()`

### UI-Rendering
**Zeile ~800-1000**: `app.rendern()`

### Export/Import
**Zeile ~430-480**: `datenExportieren()` / `datenImportieren()`

---

## 💾 Backup-Strategie

### Für Entwickler
1. Git-Repository empfohlen
2. Regelmäßige Commits
3. Tag pro Version

### Für Nutzer
1. Monatlicher Export empfohlen
2. Dateiname enthält Datum
3. Cloud-Backup (Dropbox, Drive)

---

## ⚠️ Bekannte Limitierungen

1. **LocalStorage**: Max ~5-10 MB (Browser-abhängig)
2. **Keine Saison**: Nur Jahresplanung, keine Früh-/Spätkultur
3. **Ein Beet = Eine Nutzung**: Nachkultur nicht möglich
4. **Statische Regeln**: Mischkultur hardcoded
5. **Keine Collaboration**: Single-User-System

---

## 📞 Typische User-Probleme

### "Vorschläge funktionieren nicht"
→ Prüfe: Wunschliste gefüllt? Genug Beete?

### "Daten sind weg"
→ LocalStorage gelöscht? → Aus Backup importieren

### "Kann nicht exportieren"
→ Browser-Popup-Blocker? → Erlauben

### "Matrix zeigt alles neutral"
→ Begleiter-Daten fehlen → Datenbank prüfen

---

## 🎓 Lernressourcen

### Mischkultur-Theorie
- Pflanzenfamilien und Rotation
- Nährstoffbedarf (Stark-/Mittel-/Schwachzehrer)
- Allelopathie (chemische Wechselwirkungen)
- Bodenmüdigkeit vermeiden

### Coding-Patterns
- **Model-View-Controller**: Trennung von Daten/Logik/UI
- **Repository Pattern**: GartenManager als zentrale Datenquelle
- **Strategy Pattern**: VorschlagsEngine austauschbar
- **Serialization**: toJSON/fromJSON für alle Klassen

---

## 🏁 Deployment

### Option 1: Statische Datei
- Upload auf Webserver
- Funktioniert sofort (keine Backend nötig)

### Option 2: GitHub Pages
```bash
git init
git add gartenplaner-deutsch.html
git commit -m "Initial commit"
git push origin main
# → Aktiviere GitHub Pages in Repo-Settings
```

### Option 3: Netlify/Vercel
- Drag & Drop der HTML-Datei
- Automatisches HTTPS

---

## 🔐 Sicherheit

### Keine Risiken
- Kein Server-Contact
- Keine API-Calls
- Keine Cookies/Tracking
- Keine Passwörter

### Best Practices
- RegEx-Validierung bei Import (verhindert XSS)
- JSON.parse in try-catch (verhindert Crashes)
- Kein eval() verwendet

---

## 📈 Performance-Optimierung

### Aktuelle Metriken
- **Dateigröße**: ~80 KB
- **Ladezeit**: <1s (Breitband)
- **Memory**: ~5-10 MB (mit Daten)

### Optimierungspotenzial
- [ ] Minifizierung (→ ~40 KB)
- [ ] Lazy Loading von Matrix
- [ ] Virtual Scrolling bei >20 Beeten
- [ ] Service Worker (Offline-Fähigkeit)

---

## ✅ Pre-Release Checklist

Vor jeder neuen Version:

- [ ] Alle Funktionen manuell testen
- [ ] Export/Import mit Beispieldaten
- [ ] Browser-Kompatibilität (Chrome, Firefox, Safari)
- [ ] Mobile-Ansicht testen
- [ ] LocalStorage-Limits testen (>100 Beete)
- [ ] Code-Kommentare aktualisieren
- [ ] Versionsnummer in HTML ändern
- [ ] CHANGELOG.md aktualisieren

---

**Letzte Aktualisierung**: 2025  
**Version**: 1.0  
**Entwickelt für**: Private Gemüsegärtner  
**Wartung**: Self-contained, keine Dependencies
