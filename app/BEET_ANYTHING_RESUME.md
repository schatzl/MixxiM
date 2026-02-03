# BEET ANYTHING - Entwickler-Resume v1.0 PWA

## 🎯 Schnellstart

**Produktname**: Beet Anything  
**Version**: 1.0 PWA (Progressive Web App)  
**Datei**: `gartenplaner-deutsch.html` (~95 KB)  
**Typ**: Single-Page-Application (Self-contained)  
**Sprache**: Vollständig Deutsch  
**Status**: Production Ready  
**Font**: Inter von https://rsms.me/inter/

---

## 📦 Was ist implementiert

### Kern-Features (alle ✅)
✅ Mehrjahresplanung mit unbegrenzter Historie  
✅ Dynamische Beetverwaltung (unbegrenzt)  
✅ 20 deutsche Gemüsesorten mit Mischkultur-Daten  
✅ Intelligenter Vorschlagsalgorithmus (Scoring-basiert)  
✅ Kompatibilitäts-Matrix (20×20 Kombinationen)  
✅ **Auto-Save nach jeder Änderung** (kein manuelles Speichern nötig!)  
✅ **Auto-Load beim Start** (alle Daten automatisch wiederhergestellt)  
✅ Export/Import (JSON für Backups)  
✅ **PWA-Installation** (iOS, Android, Desktop)  
✅ **Offline-Funktionalität** (Service Worker)  
✅ **Mobile-optimiert** (iPhone 16, Android, alle Geräte)  
✅ Responsive Design (Desktop, Tablet, Mobile)

### Neue Features in v1.0 PWA
🆕 Automatisches Speichern (kein "Speichern"-Button nötig)  
🆕 Progressive Web App mit Installation  
🆕 Offline-Modus (funktioniert ohne Internet)  
🆕 Mobile-First Design (iPhone 16 optimiert)  
🆕 Inter Font (moderne UI-Schrift von rsms.me)  
🆕 Install-Button im Header (immer sichtbar)  
🆕 Intelligente Installations-Anleitungen  

---

## 🏗️ Architektur-Überblick

### Klassen (OOP-Hierarchie)

```
Gemuese              → Gemüsedaten + Begleiter-Logik
Gartenbeet           → Beet-Metadaten
Pflanzung            → Beet-Jahr-Gemüse-Verknüpfung
GartenManager        → Zentrale Datenverwaltung
VorschlagsEngine     → Algorithmus für optimale Zuweisung
app (Global)         → UI-Controller + Event-Handler
```

### Datenfluss

```
User Interaction
    ↓
app.* Methoden (Controller)
    ↓
GartenManager (Model)
    ↓
app.speichern() → LocalStorage (AUTO!)
    ↓
app.rendern() (View)
    ↓
DOM Update
```

---

## 🔄 Auto-Save System (WICHTIG!)

### Automatisch gespeichert nach:

| Aktion | Speicherung |
|--------|-------------|
| Beet hinzufügen | ✅ Sofort |
| Beet entfernen | ✅ Sofort |
| Beet umbenennen | ✅ Beim Modal-Speichern |
| Pflanze hinzufügen | ✅ Sofort |
| Pflanze entfernen | ✅ Sofort |
| Jahr ändern | ✅ Sofort |
| Wunschliste ändern | ✅ Sofort |
| Vorschlag anwenden | ✅ Sofort |

**KEINE manuelle Speicherung nötig!** Alles automatisch.

### LocalStorage Schlüssel

```javascript
'gartenplanerDaten'    // Hauptdaten (Beete, Pflanzungen, Gemüse)
'beetAnythingState'    // App-Status (Jahr, Wunschliste)
```

### Wichtigste App-Methoden

```javascript
app.init()                          // Initialisierung + Auto-Load
app.speichern()                     // Auto-Save (wird automatisch aufgerufen!)
app.jahrAendern(±1)                // Jahr navigieren + Auto-Save
app.vorschlaegeGenerieren()        // Algorithmus starten
app.beetModalOeffnen(beetId)       // Beet bearbeiten
app.datenExportieren()             // JSON Download (manuelles Backup)
app.datenImportieren()             // JSON Upload (Restore)
app.matrixAnzeigen()               // Mischkultur-Matrix
app.alsAppInstallieren()           // PWA-Installation triggern
app.rendern()                      // UI aktualisieren
```

---

## 📱 PWA-Features

### Installation erkennen

```javascript
// App prüft automatisch:
if (window.matchMedia('(display-mode: standalone)').matches) {
    // App läuft als PWA
    // Install-Buttons werden ausgeblendet
}
```

### Install-Button-Positionen

1. **Header-Button** (ID: `headerInstallButton`)
   - Immer sichtbar (außer wenn bereits installiert)
   - Bei "📱 Als App installieren"
   - Funktioniert auf allen Geräten

2. **Floating-Button** (ID: `floatingInstallButton`)
   - Unten rechts (Desktop)
   - Volle Breite unten (Mobile)
   - Nur wenn Browser PWA unterstützt

### Installation-Status prüfen

**Im Browser DevTools Konsole:**
```javascript
// Prüfen ob als PWA installiert:
window.matchMedia('(display-mode: standalone)').matches

// Wenn true → App ist installiert
// Wenn false → App läuft im Browser
```

**Visuelle Indikatoren:**
- ✅ Install-Button verschwunden = App ist installiert
- ✅ Keine Browser-Leiste = Läuft als PWA
- ✅ App-Icon auf Homescreen = Installiert

### Service Worker

**Cached:**
- App-Shell (HTML, CSS, JS)
- Fonts (Inter von rsms.me)

**Offline verfügbar:**
- Alle Features (Planung, Bearbeitung, Algorithmus)
- LocalStorage funktioniert offline
- Nur erste Installation braucht Internet

---

## 🧮 Algorithmus-Kernlogik

**Datei-Position**: `VorschlagsEngine.pflanzungsOptionBewerten()` (ca. Zeile 1300)

### Scoring-Gewichte:

| Kriterium | Punkte | Bedingung |
|-----------|--------|-----------|
| Familienrotation | +30 | Andere Familie als Vorjahr |
| Familienrotation | -20 | Gleiche Familie wie Vorjahr |
| Nährstoffrotation | +25 | Schwachzehrer nach Starkzehrer |
| Nährstoffrotation | -15 | Starkzehrer nach Starkzehrer |
| Nährstoffrotation | +10 | Schwachzehrer generell |
| Guter Begleiter | +15 | Pro kompatible Pflanze |
| Schlechter Begleiter | -30 | Pro inkompatible Pflanze |
| Leeres Beet | +5 | Keine aktuellen Pflanzen |
| 2-Jahres-Rotation | -10 | Gleiche Pflanze vor 2 Jahren |

**Output**: Sortierte Liste mit Beet-Gemüse-Zuweisungen + Begründungen

---

## 📊 Datenstruktur

### LocalStorage

```javascript
// Hauptdaten
localStorage.getItem('gartenplanerDaten')
{
  "gemueseSorten": [...],  // 20 Gemüsesorten
  "beete": [...],          // Alle Beete
  "pflanzungen": [...]     // Alle Pflanzungen (alle Jahre)
}

// App-State
localStorage.getItem('beetAnythingState')
{
  "aktuellesJahr": 2024,
  "wunschliste": ["tomate", "karotte"]
}
```

---

## 🎨 Design-System

### Schriftart: Inter (rsms.me)

```css
@import url('https://rsms.me/inter/inter.css');

font-family: 'Inter', sans-serif;
font-feature-settings: 'liga' 1, 'calt' 1;
```

**Gewichte:**
- 400 (Normal): Fließtext
- 700 (Bold): h2, h3
- 800 (Extra Bold): h1

### CSS-Variablen (Farbschema)

```css
--boden-dunkel: #3a2f28    /* Primärtext */
--blatt-gruen: #4a7c59     /* Primärfarbe */
--salbei: #8ba888          /* Sekundärfarbe */
--creme: #f4f1ea           /* Hintergrund */
--terrakotta: #c1694f      /* Akzent/Starkzehrer */
--sonnen-gelb: #e8b84d     /* Highlight/Mittelzehrer */
```

### Responsive Breakpoints

| Breakpoint | Layout |
|------------|--------|
| > 968px | 2-Spalten (1:2) |
| 768-968px | 1-Spalte |
| 480-768px | 1-Spalte, kompakt |
| 375-480px | 1-Spalte, mobile |
| < 375px | 1-Spalte, minimal |

**Landscape < 968px**: 2-Spalten (1:1.5)

---

## 🔧 Häufige Anpassungen

### 1. Neue Gemüsesorte hinzufügen

**Position**: `GartenManager.gemueseDatenbankInitialisieren()` (ca. Zeile 900)

```javascript
// Schritt 1: Gemüse erstellen
const gemueseListe = [
    // ... bestehende ...
    new Gemuese('rucola', 'Rucola', 'niedrig', 'Kreuzblütler'),
];

// Schritt 2: Begleiter festlegen
this.begleiterFestlegen('rucola',
    ['bohnen', 'erbsen'],     // Gute Begleiter
    []                         // Schlechte Begleiter
);
```

### 2. Scoring-Gewichte ändern

**Position**: `VorschlagsEngine.pflanzungsOptionBewerten()` (ca. Zeile 1300)

```javascript
// Familie-Rotation höher bewerten
bewertung += 50;  // statt 30

// Schlechte Begleiter strenger bewerten
bewertung -= 50;  // statt 30
```

### 3. Neue Bewertungskriterien

```javascript
// Beispiel: Sonnenbedarf
if (gem.sonnenbedarf === 'voll' && beet.sonnig) {
    bewertung += 20;
    gruende.push('Optimale Sonnenlage');
}
```

### 4. Farbschema ändern

```css
:root {
    --blatt-gruen: #2d5f3f;  /* Dunkler */
    --creme: #ffffff;        /* Weißer */
}
```

---

## 🐛 Debugging-Tipps

### LocalStorage prüfen

```javascript
// Browser-Konsole:
localStorage.getItem('gartenplanerDaten')
localStorage.getItem('beetAnythingState')

// Größe prüfen
const size = new Blob([localStorage.getItem('gartenplanerDaten')]).size;
console.log('Größe:', (size / 1024).toFixed(2), 'KB');
```

### Daten zurücksetzen

```javascript
// VORSICHT: Löscht alle Daten!
localStorage.removeItem('gartenplanerDaten');
localStorage.removeItem('beetAnythingState');
location.reload();
```

### PWA-Installation prüfen

```javascript
// Läuft als PWA?
window.matchMedia('(display-mode: standalone)').matches

// Install-Prompt verfügbar?
window.deferredPrompt !== null
```

### Auto-Save testen

```javascript
// Manuell triggern
app.speichern();

// Gespeicherte Daten ansehen
console.log(JSON.parse(localStorage.getItem('beetAnythingState')));
```

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

---

## 🔍 Wichtige Dateipositionen

### Zeilen-Referenz (ca. Angaben)

| Feature | Zeile | Beschreibung |
|---------|-------|--------------|
| Gemüse-Datenbank | ~900 | `gemueseDatenbankInitialisieren()` |
| Mischkultur-Regeln | ~950 | `begleiterFestlegen()` Aufrufe |
| Scoring-Algorithmus | ~1300 | `pflanzungsOptionBewerten()` |
| Auto-Save Logik | ~1680 | `app.speichern()` |
| Auto-Load Logik | ~1120 | `app.init()` |
| UI-Rendering | ~1450 | `app.rendern()` |
| PWA Install-Code | ~1810 | Service Worker + Install-Buttons |
| Export/Import | ~1640 | `datenExportieren()` / `datenImportieren()` |

---

## 🚀 Nächste Entwicklungsschritte

### Priorität 1 (Quick Wins)
- [ ] Mehr Gemüsesorten (Ziel: 30-40)
- [ ] Aussaat/Ernte-Kalender
- [ ] Druckfunktion für Jahresplan
- [ ] Notizfeld pro Beet
- [ ] Dark Mode

### Priorität 2 (Medium)
- [ ] Beetgrößen-Eingabe
- [ ] Flächenberechnung
- [ ] Pflanzabstände
- [ ] Bilder/Fotos pro Gemüse
- [ ] Statistiken (Erntemengen)

### Priorität 3 (Advanced)
- [ ] Grafische Beetvisualisierung (SVG/Canvas)
- [ ] Drag & Drop zwischen Beeten
- [ ] Benutzer-definierte Mischkultur-Regeln
- [ ] Cloud-Sync (optional)
- [ ] Native Mobile App

---

## 📱 Mobile Testing

### Browser DevTools

**Chrome/Edge**:
```
1. F12 → DevTools
2. Toggle device toolbar (Ctrl+Shift+M)
3. Gerät: iPhone 16 Pro (393x852)
4. Testen!
```

**Firefox**:
```
1. F12 → DevTools
2. Responsive Design Mode (Ctrl+Shift+M)
3. Viewport: 393x852
4. Testen!
```

### Echtes Gerät

**iPhone**:
1. Datei auf Netlify/GitHub Pages hosten
2. URL in Safari öffnen
3. Teilen (□↑) → "Zum Home-Bildschirm"
4. Testen als PWA

**Android**:
1. Datei hosten
2. URL in Chrome öffnen
3. "Als App installieren" klicken
4. Testen als PWA

---

## 💾 Backup-Strategie

### Für Entwickler
1. Git-Repository verwenden
2. Regelmäßige Commits
3. Tags pro Version (v1.0, v1.1, etc.)

### Für Nutzer
1. **Automatisch**: LocalStorage (bleibt erhalten)
2. **Manuell**: Monatlicher Export empfohlen
3. **Cloud**: Backup in Dropbox/Google Drive

### Export-Dateinamen
```
gartenplan-2025-02-03.json
```
(Automatischer Timestamp)

---

## ⚠️ Bekannte Limitierungen

### Funktional
1. **Keine Saison**: Nur Jahresplanung, keine Früh-/Nachkultur
2. **Keine Flächen**: Beetgröße nicht berücksichtigt
3. **Statische Regeln**: Mischkultur hardcoded
4. **Single-User**: Keine Collaboration

### Technisch
1. **LocalStorage Limit**: ~5-10 MB
2. **Keine Cloud-Sync**: Daten bleiben auf Gerät
3. **Browser-spezifisch**: PWA-Installation nicht überall

---

## 🆘 Häufige Probleme

### "Auto-Save funktioniert nicht"

**Prüfen:**
```javascript
// LocalStorage aktiviert?
typeof(Storage) !== "undefined"

// Inkognito-Modus?
// → Kein LocalStorage verfügbar

// Speicher voll?
// → Alte Daten exportieren & löschen
```

### "Daten sind weg"

**Ursachen:**
- Cache gelöscht (mit "Cookies und Websitedaten")
- Anderer Browser/Gerät
- Inkognito-Modus benutzt

**Lösung:**
- Backup-Datei importieren
- Zukünftig: Regelmäßig exportieren

### "Install-Button erscheint nicht"

**Prüfen:**
```javascript
// Bereits installiert?
window.matchMedia('(display-mode: standalone)').matches

// Browser unterstützt PWA?
// iOS: Nur Safari
// Android: Chrome, Edge, Samsung Internet
// Desktop: Chrome, Edge, Opera
```

### "App läuft nicht offline"

**Lösung:**
- Mindestens einmal mit Internet öffnen
- Service Worker muss registriert werden
- Cache wird beim ersten Besuch gefüllt

---

## 📈 Performance-Tipps

### Optimierung für viele Beete (>50)

```javascript
// Bei >100 Beeten: Rendering optimieren
// Nur sichtbare Beete rendern (Virtual Scrolling)

// Bei >1000 Pflanzungen: Indexierung
// Map-basierte Lookups statt Array-Filter
```

### LocalStorage-Größe reduzieren

```javascript
// Alte Jahre archivieren
// Jahre < 2020 in separate JSON exportieren
// Aus LocalStorage entfernen
```

---

## ✅ Pre-Release Checklist

Vor jeder neuen Version:

- [ ] Alle Features manuell testen
- [ ] Auto-Save/Load testen (5 Szenarien)
- [ ] Export/Import mit Beispieldaten
- [ ] Browser-Kompatibilität (Chrome, Firefox, Safari)
- [ ] Mobile-Ansicht testen (iPhone, Android)
- [ ] PWA-Installation testen
- [ ] Offline-Modus testen
- [ ] LocalStorage-Limits testen (>100 Beete)
- [ ] Code-Kommentare aktualisieren
- [ ] Versionsnummer in Dokumentation ändern
- [ ] CHANGELOG aktualisieren
- [ ] README aktualisieren

---

## 🎓 Für neue Entwickler

### Einstieg in 5 Minuten

1. **Datei öffnen**: `gartenplaner-deutsch.html` in Editor
2. **Nach Konzept suchen**: Ctrl+F "Gemuese" → Klasse finden
3. **Verstehen**: OOP-Hierarchie → GartenManager → VorschlagsEngine
4. **Anpassen**: Gemüse hinzufügen (siehe oben)
5. **Testen**: Datei im Browser öffnen

### Wichtigste Konzepte

1. **Klassenhierarchie**: Gemuese, Gartenbeet, Pflanzung
2. **Maps statt Arrays**: Schnellere Lookups
3. **Auto-Save System**: Nach jeder Änderung
4. **Scoring-Algorithmus**: Mehrere Kriterien kombiniert
5. **PWA**: Service Worker + Manifest

### Code-Stil

- **Deutsch für Business-Logik**: beetHinzufuegen(), gemueseSorten
- **Englisch für Technical**: Map, Array, JSON
- **Kommentare**: Wo nötig, nicht überall
- **Struktur**: Klassen → Manager → App → UI

---

## 📞 Support-Ressourcen

### Dokumentation

1. **BEET_ANYTHING_SPEZIFIKATION_V1.0_PWA.md** - Vollständig
2. **Dieses Resume** - Schnellreferenz
3. **APP_INSTALLATION_ANLEITUNG.md** - PWA-Installation
4. **AUTO_SAVE_TEST_ANLEITUNG.md** - Test-Szenarien
5. **MOBILE_OPTIMIERUNG.md** - Responsive Design

### Im Code

- JSDoc-Kommentare bei Klassen
- Inline-Kommentare bei komplexer Logik
- Trennlinien zwischen Code-Bereichen

---

## 🔐 Sicherheit

### Keine Risiken
- Kein Server-Kontakt
- Keine API-Calls
- Keine Cookies/Tracking
- Keine Passwörter

### Best Practices
- JSON.parse in try-catch
- Input-Validierung bei Import
- Kein eval() verwendet
- Keine externe Scripts (außer Inter Font)

---

## 🏁 Deployment

### Option 1: Statische Datei
```bash
# Einfach auf Webserver hochladen
# Funktioniert sofort, kein Build nötig
```

### Option 2: GitHub Pages
```bash
git init
git add gartenplaner-deutsch.html
# Umbenennen zu index.html!
mv gartenplaner-deutsch.html index.html
git commit -m "Initial commit"
git push origin main
# → GitHub Pages aktivieren
# URL: https://username.github.io/repo-name
```

### Option 3: Netlify
```bash
# Drag & Drop in Netlify
# Datei als index.html hochladen
# Automatisches HTTPS
# URL: https://beet-anything.netlify.app
```

---

## 📊 Metriken (Typische Nutzung)

| Metrik | Wert |
|--------|------|
| Dateigröße (HTML) | ~95 KB |
| Dateigröße (Minified) | ~45 KB |
| Dateigröße (Gzip) | ~20 KB |
| LocalStorage (10 Beete, 3 Jahre) | ~20 KB |
| LocalStorage (50 Beete, 10 Jahre) | ~100 KB |
| Ladezeit (WLAN) | < 1s |
| Ladezeit (4G) | < 2s |
| Ladezeit (Cached) | < 0.5s |

---

**Letzte Aktualisierung**: Februar 2025  
**Version**: 1.0 PWA  
**Status**: Production Ready  
**Entwickelt für**: Private Gemüsegärtner  
**Wartung**: Self-contained, keine Dependencies (außer Inter Font)
