# Beet Anything - Produktspezifikation

## Produktübersicht

**Produktname:** Beet Anything  
**Version:** 1.0  
**Typ:** Web-basierte Gartenplanungs-Anwendung  
**Zweck:** Intelligente Planung von Gemüsegärten unter Berücksichtigung von Fruchtfolge und Mischkultur

## Kernfunktionalität

### 1. Mehrjahresplanung
- Navigation zwischen verschiedenen Jahrgängen (Vorwärts/Rückwärts)
- Historische Pflanzungsdaten für jedes Beet und Jahr
- Anzeige der Vorjahrespflanzungen zur besseren Planung

### 2. Beete-Verwaltung
- Dynamisches Hinzufügen/Entfernen von Gartenbeeten
- Individuelle Benennung jedes Beets
- Zuweisung mehrerer Pflanzen pro Beet und Jahr
- Visuelle Darstellung aktueller und vergangener Bepflanzungen

### 3. Gemüse-Datenbank
Aktuell 20 Gemüsesorten mit folgenden Attributen:

#### Enthaltene Gemüsesorten:
- Tomate, Kartoffel, Karotte, Salat, Kohl
- Bohnen, Erbsen, Zwiebel, Knoblauch
- Gurke, Zucchini, Mais, Radieschen
- Spinat, Basilikum, Paprika, Sellerie
- Rucola, Kohlrabi, Lauch

#### Attribute pro Gemüse:
- **ID**: Eindeutiger Bezeichner
- **Name**: Deutsche Bezeichnung
- **Nährstoffbedarf**: hoch / mittel / niedrig
- **Pflanzenfamilie**: Botanische Familie (z.B. Nachtschattengewächse)
- **Gute Begleiter**: Liste kompatibler Pflanzen
- **Schlechte Begleiter**: Liste inkompatibler Pflanzen

### 4. Wunschlisten-System
- Auswahl gewünschter Gemüsesorten für das aktuelle Jahr
- Einfaches Hinzufügen/Entfernen von Gemüse
- Visuelle Tag-basierte Darstellung

### 5. Intelligenter Vorschlagsalgorithmus

#### Bewertungskriterien (Scoring-System):

**A. Familienrotation (±30 Punkte)**
- +30: Andere Pflanzenfamilie als im Vorjahr
- -20: Gleiche Pflanzenfamilie wie im Vorjahr
- Verhindert Bodenmüdigkeit und Schädlingsakkumulation

**B. Nährstoffrotation (±25 Punkte)**
- +25: Schwachzehrer nach Starkzehrer (optimal)
- +10: Schwachzehrer generell (bodenschonend)
- -15: Starkzehrer nach Starkzehrer (Bodenbelastung)

**C. Mischkultur-Kompatibilität (±30 Punkte)**
- +15: Pro guter Begleiter im selben Beet
- -30: Pro schlechter Begleiter im selben Beet

**D. Weitere Faktoren**
- +5: Leeres Beet (mehr Flexibilität)
- -10: Gleiche Pflanze vor 2 Jahren (erweiterte Rotation)

#### Algorithmus-Ablauf:
1. Berechne Bewertung für jede Gemüse-Beet-Kombination
2. Sortiere nach Bewertung (absteigend)
3. Weise Gemüse nacheinander dem bestbewerteten verfügbaren Beet zu
4. Vermeide Doppelzuweisungen

### 6. Kompatibilitäts-Matrix
- Tabellarische Übersicht aller Mischkultur-Beziehungen
- Farbcodierung:
  - ✓ Grün = Gute Begleiter
  - ✗ Rot = Schlechte Begleiter
  - ○ Grau = Neutral
- Scrollbare Ansicht für große Datenmengen

### 7. Datenpersistierung

#### LocalStorage (automatisch)
- Kontinuierliche Speicherung aller Änderungen
- Automatisches Laden beim nächsten Besuch
- Schlüssel: `gartenplanerDaten`

#### Export/Import (manuell)
- **Export**: JSON-Datei mit Timestamp im Dateinamen
- **Import**: Laden von zuvor exportierten JSON-Dateien
- **Datenstruktur**:
  - Alle Gemüsesorten mit Attributen
  - Alle Beete mit IDs und Namen
  - Alle Pflanzungen (Beet-Jahr-Gemüse-Zuordnungen)

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

### Datenstrukturen

#### JSON Export-Format:
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
    {
      "id": 1234567890,
      "name": "Beet 1"
    }
  ],
  "pflanzungen": [
    {
      "beetId": 1234567890,
      "jahr": 2024,
      "gemueseId": "tomate"
    }
  ]
}
```

## Benutzeroberfläche

### Layout-Struktur
- **Kopfbereich**: Titel, Untertitel, Daten-Steuerung (Export/Import/Matrix)
- **Linke Spalte (1/3 Breite)**:
  - Jahresnavigation
  - Wunschliste mit Gemüseauswahl
  - "Gartenplan vorschlagen" Button
  - Vorschlagsbox (dynamisch)
  - "Gartenbeet hinzufügen" Button
  - Hilfetext
- **Rechte Spalte (2/3 Breite)**:
  - Grid von Gartenbeeten
  - Responsive: 1-3 Spalten je nach Bildschirmbreite

### Farbschema
```css
--boden-dunkel: #3a2f28
--boden-mittel: #5d4e3f
--blatt-gruen: #4a7c59
--salbei: #8ba888
--creme: #f4f1ea
--terrakotta: #c1694f
--sonnen-gelb: #e8b84d
--wurzel-braun: #6b4423
--wasser-blau: #7ba8a8
```

### Typografie
- **Überschriften**: Playfair Display (Serif)
- **Fließtext**: Merriweather (Serif)
- Organische, natürliche Ästhetik passend zum Gartenthema

### Interaktive Elemente

#### Beet-Karte:
- Klick öffnet Modal zur Bearbeitung
- Zeigt aktuelle Pflanzen mit:
  - Nährstoffbedarf-Badge (farbcodiert)
  - Pflanzenfamilie
  - Gute/schlechte Begleiter (wenn vorhanden)
  - Vorjahrespflanzungen (Footer)

#### Modals:
1. **Beet-Modal**:
   - Beetname bearbeiten
   - Pflanzen hinzufügen/entfernen
   - Liste aktueller Pflanzen
   
2. **Matrix-Modal**:
   - Vollständige Kompatibilitätstabelle
   - Legende

## Entwicklungsstadien

### ✅ Stadium 1: Grundgerüst (Implementiert)
- ✅ Klassenarchitektur mit Vererbung
- ✅ Gemüse-Datenbank mit Mischkultur-Informationen
- ✅ Datenpersistierung (LocalStorage + Export/Import)

### ✅ Stadium 2: Web-Interface (Implementiert)
- ✅ Vollständige deutsche Benutzeroberfläche
- ✅ Kompatibilitäts-Matrix-Ansicht
- ✅ Beetverwaltung mit Modals

### ✅ Stadium 3: Erweiterte Features (Implementiert)
- ✅ Intelligenter Vorschlagsalgorithmus
- ✅ Mehrjahres-Fruchtfolge
- ✅ Scoring-System mit multiplen Kriterien

### 🔄 Stadium 4: Zukünftige Features (Geplant)

#### Grafische Gartenvisualisierung
- SVG/Canvas-basierte Darstellung
- Verschiedene Beetformen (rechteckig, rund, L-förmig)
- Geometrische Werkzeuge für Beetanlage
- Maßstabsgetreue Darstellung

#### Drag & Drop
- Visuelles Verschieben von Pflanzen zwischen Beeten
- Automatische Vorschläge während des Ziehens
- Visuelle Feedback-Indikatoren (grün/rot für Kompatibilität)

#### Individuelle Regelsets
- Benutzer-definierte Mischkultur-Regeln
- Anpassbare Bewertungsgewichte
- Import/Export von Regel-Konfigurationen
- Community-geteilte Regelsets

#### Erweiterte Planung
- Aussaat- und Erntekalender
- Pflanzabstände und Flächenberechnung
- Saatgut- und Materialverwaltung
- Erntemengen-Tracking

## Technische Anforderungen

### Browser-Kompatibilität
- Moderne Browser (Chrome, Firefox, Safari, Edge)
- ES6+ JavaScript-Support
- LocalStorage-Unterstützung
- CSS Grid & Flexbox

### Performance
- Einzelne HTML-Datei (Self-contained)
- Keine externen Abhängigkeiten (außer Google Fonts)
- Schnelle Ladezeit (<1s)
- Reaktive UI ohne Verzögerung

### Datengröße
- Aktuell: ~80 KB (unkomprimiert)
- Nach Minifizierung: ~40 KB geschätzt

## Erweiterbarkeit

### Neue Gemüsesorten hinzufügen:
```javascript
// In gemueseDatenbankInitialisieren()
new Gemuese('rote-beete', 'Rote Beete', 'mittel', 'Fuchsschwanzgewächse')

// Begleiter festlegen
this.begleiterFestlegen('rote-beete', 
    ['zwiebel', 'kohl', 'salat'],  // Gute Begleiter
    ['spinat', 'lauch']             // Schlechte Begleiter
);
```

### Scoring-Algorithmus anpassen:
```javascript
// In VorschlagsEngine.pflanzungsOptionBewerten()
// Gewichte ändern:
bewertung += 30;  // Familie-Rotation
bewertung += 25;  // Nährstoff-Rotation
bewertung += 15;  // Guter Begleiter
bewertung -= 30;  // Schlechter Begleiter
```

### Neue Bewertungskriterien:
```javascript
// Beispiel: Sonnenbedarf berücksichtigen
if (beetHatSchatten && gem.sonnenbedarf === 'niedrig') {
    bewertung += 20;
    gruende.push('Geeignet für schattige Lage');
}
```

## Best Practices für Verwendung

### Workflow-Empfehlung:
1. **Jahreswechsel**: Zu Beginn Jahr erhöhen
2. **Wunschliste**: Gewünschte Gemüse auswählen
3. **Vorschläge**: Algorithmus Vorschläge generieren lassen
4. **Prüfung**: Vorschläge überprüfen und anpassen
5. **Anwendung**: Vorschläge auf Beete anwenden
6. **Feintuning**: Manuelle Anpassungen über Beet-Modal
7. **Export**: Regelmäßig Daten exportieren (Backup)

### Tipps:
- Mindestens 3 Jahre Historie aufbauen für beste Ergebnisse
- Matrix konsultieren bei Unsicherheiten
- Starkzehrer und Schwachzehrer abwechseln
- Gleiche Pflanzenfamilie mindestens 3 Jahre Pause
- Mischkultur nutzen für natürlichen Pflanzenschutz

## Bekannte Einschränkungen

1. **Keine Saison-Unterscheidung**: Aktuell nur Jahresplanung
2. **Keine Flächenberechnung**: Beetgröße nicht berücksichtigt
3. **Keine Mehrfach-Bepflanzung**: Ein Beet kann nicht 2x im Jahr genutzt werden
4. **Statische Regeln**: Mischkultur-Regeln fest codiert
5. **Keine Bodenwert-Tracking**: pH-Wert, Bodentyp nicht erfasst

## Datenschutz & Speicherung

- **Keine Server-Kommunikation**: Alle Daten bleiben lokal
- **LocalStorage**: Auf Gerät gespeichert (ca. 5-10 MB Limit)
- **Keine Cookies**: Keine Tracking-Mechanismen
- **Export-Kontrolle**: Nutzer hat volle Kontrolle über Daten
- **Kein Login erforderlich**: Sofort nutzbar

## Versionierung & Updates

### Version 1.0 (Aktuell)
- Grundfunktionalität vollständig
- 20 Gemüsesorten
- Deutscher Volltext
- Export/Import
- Vorschlagsalgorithmus

### Geplante Versionen:

**Version 1.1**
- Erweiterte Gemüse-Datenbank (30+ Sorten)
- Pflanzkalender (Aussaat/Ernte-Zeiten)
- Druckfunktion für Gartenplan

**Version 2.0**
- Grafische Beetvisualisierung
- Drag & Drop Interface
- Benutzer-definierte Regeln

**Version 2.5**
- Community-Features
- Regel-Sharing
- Mehrsprachigkeit

**Version 3.0**
- Mobile App (Progressive Web App)
- Foto-Upload für Beete
- KI-gestützte Erkennung von Problemen

## Support & Dokumentation

### Inline-Hilfe
- Info-Boxen in der Anwendung
- Tooltips bei Hover
- Erklärungen in Modals

### Code-Dokumentation
- JSDoc-Kommentare für alle Klassen
- Inline-Kommentare für komplexe Logik
- README-Sektion in HTML-Datei

## Lizenz & Nutzung

- **Verwendung**: Frei für private Nutzung
- **Modifikation**: Erweiterungen erlaubt
- **Weitergabe**: Mit Namensnennung
- **Kommerziell**: Absprache erforderlich

## Kontakt & Feedback

Für Verbesserungsvorschläge:
- Neue Gemüsesorten vorschlagen
- Mischkultur-Korrekturen melden
- Feature-Requests einreichen
- Bug-Reports

---

## Schnellreferenz: Wichtigste Code-Abschnitte

### App-Initialisierung:
```javascript
app.init() // Lädt Daten, initialisiert UI
```

### Zentrale Manager-Instanz:
```javascript
app.garten // Zugriff auf GartenManager
app.vorschlagsEngine // Zugriff auf Algorithmus
```

### Hauptfunktionen:
```javascript
app.vorschlaegeGenerieren() // Startet Algorithmus
app.datenExportieren() // Download JSON
app.datenImportieren() // Upload JSON
app.matrixAnzeigen() // Zeigt Kompatibilitätsmatrix
```

### Datenstruktur-Zugriff:
```javascript
app.garten.gemueseSorten // Map aller Gemüse
app.garten.beete // Map aller Beete
app.garten.pflanzungen // Array aller Pflanzungen
```

---

**Erstellt**: 2025  
**Produktname**: Beet Anything  
**Status**: Production Ready (Version 1.0)  
**Dateiname**: gartenplaner-deutsch.html
