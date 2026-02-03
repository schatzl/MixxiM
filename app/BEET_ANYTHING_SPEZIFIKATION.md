# Beet Anything - Produktspezifikation v1.0 PWA

## Produktübersicht

**Produktname:** Beet Anything  
**Version:** 1.0 PWA (Progressive Web App)  
**Typ:** Web-basierte Gartenplanungs-Anwendung mit App-Installation  
**Zweck:** Intelligente Planung von Gemüsegärten unter Berücksichtigung von Fruchtfolge und Mischkultur  
**Plattformen:** Web, iOS (Safari), Android (Chrome), Desktop (alle Browser)

## Kernfunktionalität

### 1. Mehrjahresplanung
- Navigation zwischen verschiedenen Jahrgängen (Vorwärts/Rückwärts)
- Historische Pflanzungsdaten für jedes Beet und Jahr
- Anzeige der Vorjahrespflanzungen zur besseren Planung
- Unbegrenzte Jahres-Historie (begrenzt nur durch Speicherplatz)

### 2. Beete-Verwaltung
- Dynamisches Hinzufügen/Entfernen von Gartenbeeten
- Individuelle Benennung jedes Beets
- Zuweisung mehrerer Pflanzen pro Beet und Jahr
- Visuelle Darstellung aktueller und vergangener Bepflanzungen
- Unbegrenzte Anzahl von Beeten möglich

### 3. Gemüse-Datenbank
Aktuell 20 Gemüsesorten mit folgenden Attributen:

#### Enthaltene Gemüsesorten:
- Tomate, Kartoffel, Karotte, Salat, Kohl
- Bohnen, Erbsen, Zwiebel, Knoblauch
- Gurke, Zucchini, Mais, Radieschen
- Spinat, Basilikum, Paprika, Sellerie
- Rucola, Kohlrabi, Lauch

#### Attribute pro Gemüse:
- **ID**: Eindeutiger Bezeichner (lowercase, z.B. "tomate")
- **Name**: Deutsche Bezeichnung (z.B. "Tomate")
- **Nährstoffbedarf**: hoch / mittel / niedrig
- **Pflanzenfamilie**: Botanische Familie (z.B. Nachtschattengewächse)
- **Gute Begleiter**: Array von kompatiblen Pflanzen-IDs
- **Schlechte Begleiter**: Array von inkompatiblen Pflanzen-IDs

### 4. Wunschlisten-System
- Auswahl gewünschter Gemüsesorten für das aktuelle Jahr
- Einfaches Hinzufügen/Entfernen von Gemüse
- Visuelle Tag-basierte Darstellung
- Automatische Speicherung der Wunschliste

### 5. Intelligenter Vorschlagsalgorithmus

#### Bewertungskriterien (Scoring-System):

**A. Familienrotation (±30 Punkte)**
- +30: Andere Pflanzenfamilie als im Vorjahr
- -20: Gleiche Pflanzenfamilie wie im Vorjahr
- Verhindert Bodenmüdigkeit und Schädlingsakkumulation

**B. Nährstoffrotation (±25 Punkte)**
- +25: Schwachzehrer nach Starkzehrer (optimal für Bodenregeneration)
- +10: Schwachzehrer generell (bodenschonend)
- -15: Starkzehrer nach Starkzehrer (Bodenbelastung)

**C. Mischkultur-Kompatibilität (±30 Punkte)**
- +15: Pro guter Begleiter im selben Beet (Synergien)
- -30: Pro schlechter Begleiter im selben Beet (Konkurrenz/Allelopathie)

**D. Weitere Faktoren**
- +5: Leeres Beet (mehr Flexibilität für Planung)
- -10: Gleiche Pflanze vor 2 Jahren (erweiterte Rotation)

#### Algorithmus-Ablauf:
1. Berechne Bewertung für jede Gemüse-Beet-Kombination
2. Sortiere nach Bewertung (absteigend)
3. Weise Gemüse nacheinander dem bestbewerteten verfügbaren Beet zu
4. Vermeide Doppelzuweisungen (jedes Gemüse nur einmal, jedes Beet nur einmal)
5. Generiere Begründungen für jede Empfehlung

### 6. Kompatibilitäts-Matrix
- Tabellarische Übersicht aller Mischkultur-Beziehungen
- Zeigt alle 20×20 Kombinationen
- Farbcodierung:
  - ✓ Grün = Gute Begleiter (fördern sich gegenseitig)
  - ✗ Rot = Schlechte Begleiter (hemmen sich gegenseitig)
  - ○ Grau = Neutral (keine bekannten Wechselwirkungen)
- Scrollbare Ansicht für große Datenmengen
- Sticky Header (bleibt beim Scrollen sichtbar)

### 7. Datenpersistierung

#### A. Automatisches Speichern (LocalStorage)
**Gespeichert nach jeder Aktion:**
- Beet hinzufügen/entfernen/umbenennen
- Pflanze zu Beet hinzufügen/entfernen
- Jahr ändern
- Wunschliste ändern
- Vorschlag anwenden

**Zwei LocalStorage-Schlüssel:**
1. `gartenplanerDaten` - Hauptdaten (Gemüse, Beete, Pflanzungen)
2. `beetAnythingState` - App-Zustand (Jahr, Wunschliste)

**Automatisches Laden:**
- Beim App-Start werden alle Daten wiederhergestellt
- Keine manuelle Aktion erforderlich
- Erhält vollständige Historie

#### B. Manueller Export/Import (JSON)
- **Export**: Download als JSON-Datei mit Timestamp
- **Import**: Upload von JSON-Dateien
- **Verwendung**: Backups, Geräte-Wechsel, Teilen mit anderen
- **Datenstruktur**: Vollständiges JSON mit allen Gemüsen, Beeten, Pflanzungen

### 8. Progressive Web App (PWA) Features

#### Installation
- **iOS (Safari)**: "Zum Home-Bildschirm" über Teilen-Menü
- **Android (Chrome)**: Automatischer Install-Prompt oder Menü
- **Desktop**: Browser-Install-Prompt (Chrome, Edge, Opera)

#### Install-Button Positionen:
1. **Header-Button**: Immer sichtbar bei "📱 Als App installieren"
2. **Floating-Button**: Unten rechts (nur wenn Browser PWA unterstützt)

#### Verhalten nach Installation:
- ✅ Vollbild-Modus (keine Browser-Leiste)
- ✅ App-Icon auf Homescreen/Desktop
- ✅ Schnellerer Start (aus Cache)
- ✅ Offline-Funktionalität
- ✅ App erscheint in App-Switcher
- ✅ Install-Buttons werden ausgeblendet

#### Offline-Funktionalität
- **Service Worker**: Cached App-Shell
- **Alle Features offline verfügbar**: Planung, Bearbeitung, Algorithmus
- **LocalStorage**: Funktioniert offline
- **Nur für erste Installation nötig**: Internetverbindung

#### Installation erkennen:
```javascript
// App prüft automatisch ob als PWA installiert:
if (window.matchMedia('(display-mode: standalone)').matches) {
    // Install-Buttons werden ausgeblendet
    // App läuft als PWA
}
```

**Sichtbare Indikatoren:**
- Install-Button verschwindet nach Installation
- Browser-Leiste fehlt im Vollbild-Modus
- App-Icon auf Homescreen/Desktop vorhanden

---

## Technische Architektur

### Klassenhierarchie

```
Gemuese
├── id: string
├── name: string
├── naehrstoffbedarf: 'hoch' | 'mittel' | 'niedrig'
├── familie: string
├── guteBegleiter: string[]
├── schlechteBegleiter: string[]
└── Methoden:
    ├── gutenBegleiterHinzufuegen(id)
    ├── schlechtenBegleiterHinzufuegen(id)
    ├── istKompatibel(id): -1 | 0 | 1
    ├── toJSON()
    └── fromJSON(data)

Gartenbeet
├── id: number (timestamp)
├── name: string
└── Methoden:
    ├── toJSON()
    └── fromJSON(data)

Pflanzung
├── beetId: number
├── jahr: number
├── gemueseId: string
└── Methoden:
    ├── toJSON()
    └── fromJSON(data)

GartenManager
├── gemueseSorten: Map<string, Gemuese>
├── beete: Map<number, Gartenbeet>
├── pflanzungen: Pflanzung[]
└── Methoden:
    ├── gemueseDatenbankInitialisieren()
    ├── begleiterFestlegen(id, gut[], schlecht[])
    ├── beetHinzufuegen(name)
    ├── beetEntfernen(id)
    ├── pflanzungHinzufuegen(beetId, jahr, gemueseId)
    ├── pflanzungEntfernen(beetId, jahr, gemueseId)
    ├── pflanzungenFuerBeet(beetId, jahr)
    ├── pflanzungIdsFuerBeet(beetId, jahr)
    ├── datenExportieren(): JSON
    ├── datenImportieren(json): boolean
    ├── inLocalStorageSpeichern()
    └── ausLocalStorageLaden(): boolean

VorschlagsEngine
├── garten: GartenManager
└── Methoden:
    ├── vorschlaegeGenerieren(wunschliste, jahr)
    └── pflanzungsOptionBewerten(beetId, gemueseId, jahr)
```

### App-Controller (Globales Objekt)

```javascript
app
├── garten: GartenManager
├── vorschlagsEngine: VorschlagsEngine
├── aktuellesJahr: number
├── wunschliste: string[]
└── Methoden:
    ├── init()
    ├── jahrAendern(delta)
    ├── zurWunschlisteHinzufuegen()
    ├── vonWunschlisteEntfernen(gemueseId)
    ├── beetHinzufuegen()
    ├── beetEntfernen(beetId)
    ├── beetModalOeffnen(beetId)
    ├── pflanzeZuBeetHinzufuegen(beetId)
    ├── pflanzeVonBeetEntfernen(beetId, gemueseId)
    ├── beetSpeichern(beetId)
    ├── vorschlaegeGenerieren()
    ├── vorschlagAnwenden(beetId, gemueseId)
    ├── matrixAnzeigen()
    ├── matrixModalSchliessen()
    ├── datenExportieren()
    ├── datenImportieren()
    ├── alsAppInstallieren()
    ├── zeigeInstallationsAnleitung()
    ├── speichern()
    └── rendern()
```

---

## Benutzeroberfläche

### Layout-Struktur

**Desktop (> 968px):**
```
┌─────────────────────────────────────────────────┐
│ Header: Titel + Buttons (Export/Import/Matrix)  │
├───────────────┬─────────────────────────────────┤
│ Steuerung     │ Gartenbeete                     │
│ (1/3 Breite) │ (2/3 Breite)                    │
│               │                                 │
│ - Jahr        │ ┌────┐ ┌────┐ ┌────┐          │
│ - Wunschliste │ │Beet│ │Beet│ │Beet│          │
│ - Vorschläge  │ │ 1  │ │ 2  │ │ 3  │          │
│ - Beet +      │ └────┘ └────┘ └────┘          │
└───────────────┴─────────────────────────────────┘
```

**Mobile (< 480px):**
```
┌───────────────────┐
│ Header            │
│ Titel             │
│ [Button]          │
│ [Button]          │
│ [Button]          │
│ [Install]         │
├───────────────────┤
│ Steuerung         │
│ - Jahr            │
│ - Wunschliste     │
│ - Vorschläge      │
│ - Beet +          │
├───────────────────┤
│ Gartenbeete       │
│ ┌───────────────┐ │
│ │ Beet 1        │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │ Beet 2        │ │
│ └───────────────┘ │
└───────────────────┘
```

### Farbschema (Erdige Töne)
```css
--boden-dunkel: #3a2f28    /* Primärtext, dunkle Akzente */
--boden-mittel: #5d4e3f    /* Sekundärtext, Rahmen */
--blatt-gruen: #4a7c59     /* Primärfarbe, Überschriften */
--salbei: #8ba888          /* Sekundärfarbe, helle Akzente */
--creme: #f4f1ea           /* Hintergrund, Flächen */
--terrakotta: #c1694f      /* Akzentfarbe, Starkzehrer */
--sonnen-gelb: #e8b84d     /* Highlight, Mittelzehrer */
--wurzel-braun: #6b4423    /* Dunkle Akzente */
--wasser-blau: #7ba8a8     /* Info-Bereiche */
```

### Typografie

**Schriftart:** Inter (von rsms.me)
- **Quelle**: https://rsms.me/inter/
- **Typ**: Variable Sans-Serif, optimiert für UI
- **Features**: Ligaturen, kontextuelle Alternativen
- **Fallback**: System-Schriften (-apple-system, etc.)

**Gewichte:**
- 400 (Normal): Fließtext, Formulare
- 700 (Bold): h2, h3, Panel-Titel
- 800 (Extra Bold): h1, Haupt-Überschrift

**Font-Features aktiviert:**
```css
font-feature-settings: 'liga' 1, 'calt' 1;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
```

### Responsive Breakpoints

| Breakpoint | Zielgeräte | Layout | Besonderheiten |
|------------|------------|--------|----------------|
| > 968px | Desktop | 2-Spalten (1:2) | Volle Features |
| 768-968px | Tablets | 1-Spalte | Reduzierte Abstände |
| 480-768px | Große Phones | 1-Spalte | Kompaktere UI |
| 375-480px | Standard Phones | 1-Spalte | Mobile-optimiert |
| < 375px | Kleine Phones (SE) | 1-Spalte | Minimales Padding |

**Landscape Mode (Querformat < 968px):**
- 2-Spalten Layout (1:1.5)
- Steuerung links, Beete rechts
- Kompakteres Spacing

### Mobile-Optimierungen

**Touch-Targets:**
- Mindestgröße: 44×44px (Apple Guidelines)
- Großzügige Abstände zwischen Buttons
- Größere Klickbereiche

**Horizontal-Scroll Prevention:**
```css
body, html {
    overflow-x: hidden;
    max-width: 100vw;
}
* {
    max-width: 100%;
}
```

**Responsive Elemente:**
- Buttons: Volle Breite auf Mobile
- Dropdown + Button: Gestapelt statt nebeneinander
- Modals: 95% Breite auf Mobile
- Tabellen: Horizontal scrollbar bei Bedarf

---

## Datenstrukturen

### JSON Export-Format

```json
{
  "gemueseSorten": [
    {
      "id": "tomate",
      "name": "Tomate",
      "naehrstoffbedarf": "hoch",
      "familie": "Nachtschattengewächse",
      "guteBegleiter": ["basilikum", "karotte", "salat"],
      "schlechteBegleiter": ["kartoffel", "kohl"]
    }
  ],
  "beete": [
    {
      "id": 1704636800000,
      "name": "Beet 1"
    }
  ],
  "pflanzungen": [
    {
      "beetId": 1704636800000,
      "jahr": 2024,
      "gemueseId": "tomate"
    }
  ]
}
```

### LocalStorage State-Format

```json
{
  "aktuellesJahr": 2024,
  "wunschliste": ["tomate", "karotte", "salat"]
}
```

---

## PWA Manifest (inline als base64)

```json
{
  "name": "Beet Anything",
  "short_name": "Beet Anything",
  "description": "Intelligente Gartenplanung mit Fruchtfolge und Mischkultur",
  "start_url": "./",
  "display": "standalone",
  "background_color": "#f4f1ea",
  "theme_color": "#4a7c59",
  "orientation": "any",
  "icons": [
    {
      "src": "data:image/svg+xml,...",
      "sizes": "192x192",
      "type": "image/svg+xml",
      "purpose": "any maskable"
    },
    {
      "src": "data:image/svg+xml,...",
      "sizes": "512x512",
      "type": "image/svg+xml",
      "purpose": "any maskable"
    }
  ]
}
```

**Icons:** SVG mit 🌱 Emoji auf grünem Hintergrund

---

## Entwicklungsstadien

### ✅ Stadium 1: Grundgerüst (Implementiert)
- ✅ Klassenarchitektur mit Vererbung
- ✅ Gemüse-Datenbank mit Mischkultur-Informationen
- ✅ Datenpersistierung (LocalStorage + Export/Import)

### ✅ Stadium 2: Web-Interface (Implementiert)
- ✅ Vollständige deutsche Benutzeroberfläche
- ✅ Kompatibilitäts-Matrix-Ansicht
- ✅ Beetverwaltung mit Modals
- ✅ Responsive Design (Desktop + Mobile)

### ✅ Stadium 3: Erweiterte Features (Implementiert)
- ✅ Intelligenter Vorschlagsalgorithmus
- ✅ Mehrjahres-Fruchtfolge
- ✅ Scoring-System mit multiplen Kriterien
- ✅ Automatisches Speichern/Laden
- ✅ PWA-Installation
- ✅ Offline-Funktionalität
- ✅ Mobile-Optimierung (iPhone 16, Android)

### 🔄 Stadium 4: Zukünftige Features (Geplant)

#### Grafische Gartenvisualisierung
- SVG/Canvas-basierte Darstellung
- Verschiedene Beetformen (rechteckig, rund, L-förmig)
- Geometrische Werkzeuge für Beetanlage
- Maßstabsgetreue Darstellung mit Größenangaben

#### Drag & Drop
- Visuelles Verschieben von Pflanzen zwischen Beeten
- Automatische Vorschläge während des Ziehens
- Visuelle Feedback-Indikatoren (grün/rot für Kompatibilität)
- Touch-optimiert für Mobile

#### Individuelle Regelsets
- Benutzer-definierte Mischkultur-Regeln
- Anpassbare Bewertungsgewichte im Algorithmus
- Import/Export von Regel-Konfigurationen
- Community-geteilte Regelsets

#### Erweiterte Planung
- Aussaat- und Erntekalender mit Zeitfenstern
- Pflanzabstände und Flächenberechnung
- Saatgut- und Materialverwaltung
- Erntemengen-Tracking und Statistiken
- Wetterintegration (Frost-Warnungen, etc.)

#### Erweiterte Gemüse-Datenbank
- 50+ Gemüsesorten
- Kräuter und Blumen
- Sorten-Varianten (z.B. verschiedene Tomatensorten)
- Anbau-Anleitungen pro Gemüse
- Bilder/Fotos

---

## Technische Anforderungen

### Browser-Kompatibilität

**Vollständig unterstützt:**
- Chrome/Edge 90+ (Desktop & Mobile)
- Safari 14+ (Desktop & Mobile)
- Firefox 88+ (Desktop & Mobile)
- Opera 76+
- Samsung Internet 14+

**PWA-Installation:**
- Chrome/Edge (Desktop & Android): Voller Support
- Safari iOS 11.3+: Voller Support
- Firefox: Keine PWA-Installation (nur Web-Nutzung)

**Mindestanforderungen:**
- ES6+ JavaScript Support
- LocalStorage API
- CSS Grid & Flexbox
- Service Worker (für PWA)

### Performance

**Ladezeiten:**
- WLAN: < 1 Sekunde
- 4G: < 2 Sekunden
- 3G: < 5 Sekunden
- Cached (nach Installation): < 0.5 Sekunden

**Dateigröße:**
- HTML (unkomprimiert): ~90 KB
- Mit Service Worker: ~95 KB
- Nach Minifizierung: ~45 KB geschätzt
- Gzip-komprimiert: ~20 KB geschätzt

**LocalStorage:**
- Typische Nutzung: 5-50 KB
- Bei 10 Beeten, 3 Jahre: ~20 KB
- Bei 50 Beeten, 10 Jahre: ~100 KB
- Limit: 5-10 MB (Browser-abhängig)

### Abhängigkeiten

**Externe Ressourcen:**
- ✅ Inter Font (https://rsms.me/inter/inter.css)

**Keine anderen Abhängigkeiten:**
- ❌ Kein Framework (React, Vue, Angular)
- ❌ Keine UI-Library (Bootstrap, Tailwind)
- ❌ Keine Build-Tools nötig
- ❌ Kein Backend/Server erforderlich

**Vorteile:**
- Einfaches Deployment (nur HTML-Datei)
- Keine Build-Pipeline nötig
- Funktioniert überall (auch offline)
- Volle Kontrolle über Code

---

## Datenschutz & Sicherheit

### Datenspeicherung
- **100% lokal**: Alle Daten bleiben im Browser/Gerät
- **Kein Server**: Keine Datenübertragung ins Internet
- **Kein Tracking**: Keine Analytics, Cookies, oder Tracking
- **Keine Accounts**: Kein Login, keine Registrierung

### Sensible Daten
- **Keine persönlichen Daten**: Nur Gartenplanungsdaten
- **Keine Zahlungsdaten**: Kostenlose Nutzung
- **Keine Standortdaten**: Keine GPS-Nutzung

### Datenverlust-Szenarien

**Daten bleiben erhalten:**
- ✅ Browser/Tab schließen
- ✅ Computer neu starten
- ✅ Browser-Updates
- ✅ PWA-App-Updates

**Daten gehen verloren:**
- ❌ Browser-Cache komplett leeren (mit "Cookies und Websitedaten")
- ❌ LocalStorage manuell löschen
- ❌ Browser deinstallieren
- ❌ Inkognito-/Private-Browsing-Modus
- ❌ PWA-App deinstallieren (gerätespezifisch)

**Schutzmaßnahmen:**
- Regelmäßige Exports empfohlen (monatlich)
- Backup in Cloud speichern (Dropbox, Google Drive)
- Export vor größeren System-Änderungen

---

## Erweiterbarkeit

### Neue Gemüsesorte hinzufügen

**Datei:** `gartenplaner-deutsch.html`  
**Position:** `GartenManager.gemueseDatenbankInitialisieren()` (ca. Zeile 900)

```javascript
// Schritt 1: Gemüse zur Liste hinzufügen
const gemueseListe = [
    // ... bestehende Gemüse ...
    new Gemuese('rote-beete', 'Rote Beete', 'mittel', 'Fuchsschwanzgewächse'),
];

// Schritt 2: Begleiter festlegen
this.begleiterFestlegen('rote-beete',
    ['zwiebel', 'kohl', 'salat'],  // Gute Begleiter
    ['spinat', 'lauch']             // Schlechte Begleiter
);
```

### Scoring-Algorithmus anpassen

**Datei:** `gartenplaner-deutsch.html`  
**Position:** `VorschlagsEngine.pflanzungsOptionBewerten()` (ca. Zeile 1300)

```javascript
// Gewichte ändern:
bewertung += 50;  // Familienrotation (statt 30)
bewertung += 30;  // Nährstoffrotation (statt 25)
bewertung += 20;  // Guter Begleiter (statt 15)
bewertung -= 40;  // Schlechter Begleiter (statt 30)
```

### Neue Bewertungskriterien hinzufügen

```javascript
// Beispiel: Sonnenbedarf berücksichtigen
if (gem.sonnenbedarf === 'voll' && beet.lage === 'süden') {
    bewertung += 20;
    gruende.push('Optimale Sonneneinstrahlung');
}
```

### UI-Anpassungen

**Farbschema ändern:**
```css
:root {
    --blatt-gruen: #2d5f3f;  /* Dunkler grün */
    --creme: #ffffff;        /* Weißer Hintergrund */
}
```

**Schriftgrößen anpassen:**
```css
body {
    font-size: 1.1rem;  /* Größer (statt 1rem) */
}
```

---

## Best Practices für Nutzung

### Empfohlener Workflow

1. **Jahresbeginn**: Jahr auf aktuelles Jahr setzen
2. **Wunschliste**: Gewünschte Gemüse für die Saison auswählen
3. **Vorschläge generieren**: Algorithmus Empfehlungen erstellen lassen
4. **Vorschläge prüfen**: Begründungen lesen, anpassen wenn nötig
5. **Anwenden**: Vorschläge mit einem Klick übernehmen
6. **Feintuning**: Manuelle Anpassungen über Beet-Modals
7. **Saisonende**: Jahr weiterschalten, Geschichte bleibt erhalten
8. **Backup**: Monatlich Daten exportieren

### Tipps für beste Ergebnisse

**Fruchtfolge:**
- Mindestens 3 Jahre Historie aufbauen
- Gleiche Pflanzenfamilie mindestens 3 Jahre Pause
- Starkzehrer und Schwachzehrer abwechseln

**Mischkultur:**
- Matrix konsultieren bei Unsicherheiten
- Mehrere gute Begleiter pro Beet kombinieren
- Schlechte Begleiter unbedingt vermeiden

**Planung:**
- Wunschliste realistisch halten (weniger = besser)
- Mehr Beete = flexiblere Planung
- Vorschläge als Ausgangspunkt, nicht als Dogma

**Datensicherheit:**
- Export nach jeder größeren Planungsänderung
- Backup vor Browser-Wartung
- Cloud-Speicherung für Langzeit-Backup

---

## Bekannte Einschränkungen

### Funktional
1. **Keine Saison-Unterscheidung**: Nur Jahresplanung, keine Früh-/Spät-/Nachkultur
2. **Keine Flächenberechnung**: Beetgröße wird nicht berücksichtigt
3. **Keine Mehrfach-Bepflanzung**: Ein Beet kann nicht mehrmals im Jahr genutzt werden
4. **Statische Mischkultur-Regeln**: Fest codiert, nicht anpassbar (außer im Code)
5. **Kein Bodenwert-Tracking**: pH-Wert, Bodentyp nicht erfasst

### Technisch
1. **LocalStorage-Limit**: ~5-10 MB (Browser-abhängig)
2. **Keine Cloud-Sync**: Daten bleiben auf einem Gerät
3. **Keine Collaboration**: Kein Mehrbenutzerbetrieb
4. **Browser-spezifisch**: PWA-Installation nur in unterstützten Browsern

### Design
1. **Feste Gemüse-Liste**: Nur 20 vordefinierte Sorten
2. **Keine Bilder**: Nur Text und Icons
3. **Keine Karten-Ansicht**: Keine geografische Beetdarstellung

---

## Versionierung

### Version 1.0 PWA (Aktuell)
- ✅ Vollständige Grundfunktionalität
- ✅ 20 Gemüsesorten
- ✅ Deutscher Volltext
- ✅ Auto-Save/Auto-Load
- ✅ Export/Import
- ✅ Vorschlagsalgorithmus
- ✅ PWA-Installation
- ✅ Offline-Funktionalität
- ✅ Mobile-Optimierung (iPhone/Android)
- ✅ Inter Font (rsms.me)

### Geplante Versionen

**Version 1.1** (Q2 2025)
- Erweiterte Gemüse-Datenbank (30+ Sorten)
- Pflanzkalender (Aussaat/Ernte-Zeiten)
- Druckfunktion für Gartenplan
- Notizfeld pro Beet

**Version 2.0** (Q4 2025)
- Grafische Beetvisualisierung
- Drag & Drop Interface
- Benutzer-definierte Regeln
- Beetgrößen und Flächenberechnung

**Version 2.5** (2026)
- Community-Features
- Regel-Sharing
- Mehrsprachigkeit (EN, FR)
- Erweiterte Statistiken

**Version 3.0** (2027)
- Native Mobile App (Flutter/React Native)
- Cloud-Synchronisation (optional)
- Foto-Upload für Beete
- KI-gestützte Problemerkennung

---

## Support & Dokumentation

### Verfügbare Dokumentation

1. **BEET_ANYTHING_SPEZIFIKATION.md** (dieses Dokument)
   - Vollständige Produktbeschreibung
   - Technische Details
   - Erweiterbarkeit

2. **BEET_ANYTHING_RESUME.md**
   - Schnellreferenz für Entwickler
   - Code-Positionen
   - Häufige Anpassungen

3. **APP_INSTALLATION_ANLEITUNG.md**
   - PWA-Installation auf allen Plattformen
   - Schritt-für-Schritt-Anleitungen
   - Troubleshooting

4. **AUTO_SAVE_TEST_ANLEITUNG.md**
   - Test-Szenarien für Auto-Save
   - Debugging-Tipps
   - Datensicherheits-Hinweise

5. **MOBILE_OPTIMIERUNG.md**
   - Responsive Design Details
   - Mobile-spezifische Features
   - Testing-Anleitung

### Inline-Hilfe in der App

- Info-Boxen in Panels
- Tooltips bei Hover (Desktop)
- Erklärungen in Modals
- Vorschläge mit Begründungen

### Code-Dokumentation

- JSDoc-Kommentare für alle Klassen
- Inline-Kommentare für komplexe Logik
- Deutsche Methodennamen für Business-Logik
- Strukturierte Code-Bereiche mit Trennlinien

---

## Lizenz & Nutzung

**Nutzungsrechte:**
- ✅ Frei für private Nutzung
- ✅ Modifikation erlaubt
- ✅ Weitergabe mit Namensnennung
- ⚠️ Kommerzielle Nutzung nur nach Absprache

**Open Source:**
- Code ist einsehbar (Single-HTML-Datei)
- Keine Verschlüsselung oder Obfuskation
- Community-Beiträge willkommen

**Haftung:**
- Keine Garantie für Richtigkeit der Anbauempfehlungen
- Nutzung auf eigene Verantwortung
- Keine Haftung für Ernteverluste

---

## Kontakt & Feedback

**Verbesserungsvorschläge:**
- Neue Gemüsesorten vorschlagen
- Mischkultur-Korrekturen melden
- Feature-Requests einreichen
- Bug-Reports

**Datenqualität:**
- Gemüse-Datenbank basiert auf allgemeinem Gartenwissen
- Regionale Unterschiede möglich
- Empirische Anpassungen empfohlen

---

## Schnellreferenz: Dateistruktur

```
beet-anything/
├── gartenplaner-deutsch.html          (Haupt-App, ~95 KB)
├── BEET_ANYTHING_SPEZIFIKATION.md     (dieses Dokument)
├── BEET_ANYTHING_RESUME.md            (Entwickler-Schnellstart)
├── APP_INSTALLATION_ANLEITUNG.md      (PWA-Installation)
├── AUTO_SAVE_TEST_ANLEITUNG.md        (Auto-Save Tests)
└── MOBILE_OPTIMIERUNG.md              (Mobile Features)
```

---

## Technischer Stack - Zusammenfassung

| Komponente | Technologie | Version |
|------------|-------------|---------|
| Frontend | Pure HTML/CSS/JS | ES6+ |
| Styling | Custom CSS | CSS3 |
| Layout | CSS Grid + Flexbox | - |
| Font | Inter (rsms.me) | Variable Font |
| Persistierung | LocalStorage API | - |
| PWA | Service Worker | - |
| Offline | Cache API | - |
| Icons | SVG + Emoji | - |
| Build | Keine Tools nötig | - |
| Hosting | Statischer Webserver | - |

**Keine externen JavaScript-Libraries!**

---

**Erstellt**: 2025  
**Produktname**: Beet Anything  
**Version**: 1.0 PWA  
**Status**: Production Ready  
**Dateiname**: gartenplaner-deutsch.html  
**Letzte Aktualisierung**: Februar 2025
