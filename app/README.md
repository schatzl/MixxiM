# Auto-Save / Auto-Load Test-Anleitung

## ✅ Bestätigung: Alles wird automatisch gespeichert!

**Beet Anything** speichert ALLE Daten automatisch nach jeder Änderung. Sie müssen nichts manuell speichern!

---

## 🔄 Was wird automatisch gespeichert?

### Beim Start der App (Auto-Load):
✅ Alle Gartenbeete mit Namen  
✅ Alle Pflanzungen (Beet-Jahr-Gemüse-Zuweisungen)  
✅ Aktuelles Jahr  
✅ Wunschliste  
✅ Gesamte Historie (alle Jahre)  

### Nach jeder Änderung (Auto-Save):

| Aktion | Automatisch gespeichert? |
|--------|-------------------------|
| ✅ Beet hinzufügen | JA - sofort |
| ✅ Beet entfernen | JA - sofort |
| ✅ Beet umbenennen | JA - beim Speichern-Button im Modal |
| ✅ Pflanze zu Beet hinzufügen | JA - sofort |
| ✅ Pflanze von Beet entfernen | JA - sofort |
| ✅ Jahr ändern (← →) | JA - sofort |
| ✅ Gemüse zur Wunschliste | JA - sofort |
| ✅ Gemüse von Wunschliste entfernen | JA - sofort |
| ✅ Vorschlag anwenden | JA - sofort |

---

## 🧪 So testen Sie Auto-Save/Auto-Load:

### Test 1: Beete bleiben erhalten

1. **Öffnen Sie die App**
2. **Fügen Sie ein Beet hinzu**: "Mein Testbeet"
3. **Schließen Sie den Browser-Tab** (einfach Tab schließen, nicht speichern)
4. **Öffnen Sie die App erneut**
5. **✅ Ergebnis**: "Mein Testbeet" ist noch da!

### Test 2: Pflanzungen bleiben erhalten

1. **Öffnen Sie die App**
2. **Klicken Sie auf ein Beet**
3. **Fügen Sie Tomaten hinzu**
4. **Klicken Sie "Speichern" im Modal**
5. **Schließen Sie den Browser-Tab**
6. **Öffnen Sie die App erneut**
7. **✅ Ergebnis**: Tomate ist noch im Beet!

### Test 3: Jahr bleibt erhalten

1. **Öffnen Sie die App**
2. **Klicken Sie mehrmals auf →** (z.B. auf Jahr 2027)
3. **Schließen Sie den Browser-Tab**
4. **Öffnen Sie die App erneut**
5. **✅ Ergebnis**: Jahr ist noch 2027!

### Test 4: Wunschliste bleibt erhalten

1. **Öffnen Sie die App**
2. **Fügen Sie Karotte und Salat zur Wunschliste hinzu**
3. **Schließen Sie den Browser-Tab**
4. **Öffnen Sie die App erneut**
5. **✅ Ergebnis**: Karotte und Salat sind noch in der Wunschliste!

### Test 5: Historie über Jahre bleibt erhalten

1. **Öffnen Sie die App** (Jahr 2024)
2. **Beet 1**: Fügen Sie Tomate hinzu
3. **Jahr 2025**: Klicken Sie auf →
4. **Beet 1**: Fügen Sie Karotte hinzu
5. **Jahr 2026**: Klicken Sie auf →
6. **Schließen Sie den Browser-Tab**
7. **Öffnen Sie die App erneut**
8. **Navigieren Sie zurück zu 2024** (← →)
9. **✅ Ergebnis**: 
   - 2024: Tomate in Beet 1
   - 2025: Karotte in Beet 1
   - Historie ist komplett erhalten!

---

## 💾 Technische Details

### Speicher-Mechanismus:

**LocalStorage** wird verwendet mit 2 Schlüsseln:

1. **`gartenplanerDaten`** - Hauptdaten:
   ```json
   {
     "gemueseSorten": [...],
     "beete": [...],
     "pflanzungen": [...]
   }
   ```

2. **`beetAnythingState`** - App-Zustand:
   ```json
   {
     "aktuellesJahr": 2024,
     "wunschliste": ["tomate", "karotte"]
   }
   ```

### Wann wird gespeichert?

Nach **jeder** dieser Aktionen:
```javascript
this.speichern(); // Wird automatisch aufgerufen
```

Auto-Save Trigger:
- `beetHinzufuegen()` ✅
- `beetEntfernen()` ✅
- `pflanzeZuBeetHinzufuegen()` ✅
- `pflanzeVonBeetEntfernen()` ✅
- `beetSpeichern()` ✅
- `vorschlagAnwenden()` ✅
- `jahrAendern()` ✅
- `zurWunschlisteHinzufuegen()` ✅
- `vonWunschlisteEntfernen()` ✅

### Wann wird geladen?

Beim App-Start:
```javascript
app.init() {
    // 1. Lade Gartendaten
    this.garten.ausLocalStorageLaden();
    
    // 2. Lade App-State (Jahr + Wunschliste)
    const state = localStorage.getItem('beetAnythingState');
    // ... Jahr und Wunschliste wiederherstellen
}
```

---

## 🔒 Datensicherheit

### Wo werden Daten gespeichert?

- **Lokal im Browser** (LocalStorage)
- **NICHT auf einem Server**
- **NICHT in der Cloud**
- **Pro Gerät/Browser** isoliert

### Wann gehen Daten verloren?

Daten bleiben erhalten bei:
✅ Browser-Tab schließen  
✅ Browser schließen  
✅ Computer neu starten  
✅ Browser-Updates  
✅ PWA-App-Updates  

Daten gehen verloren bei:
❌ Browser-Cache leeren (mit "Cookies und Websitedaten")  
❌ LocalStorage manuell löschen  
❌ Browser komplett deinstallieren  
❌ "Private Browsing" / Inkognito-Modus  
❌ PWA-App deinstallieren  

### Schutz vor Datenverlust:

**Empfehlung**: Regelmäßig exportieren!

1. **Monatlicher Export**:
   - "💾 Daten exportieren" klicken
   - JSON-Datei wird heruntergeladen
   - In Cloud speichern (Dropbox, Google Drive)

2. **Vor größeren Änderungen**:
   - Export erstellen
   - Änderungen vornehmen
   - Bei Problemen: Import der Backup-Datei

3. **Vor Browser-Wartung**:
   - Vor Cache-Leerung: Exportieren
   - Nach Cache-Leerung: Importieren

---

## 🆘 Problembehandlung

### "Meine Daten sind weg!"

**Mögliche Ursachen**:

1. **Anderes Gerät/Browser**:
   - LocalStorage ist pro Browser/Gerät
   - **Lösung**: Export vom alten Gerät → Import auf neuem

2. **Inkognito-Modus**:
   - Private Browsing speichert nicht dauerhaft
   - **Lösung**: Normalen Browser-Modus verwenden

3. **Cache gelöscht**:
   - LocalStorage wurde mit gelöscht
   - **Lösung**: Backup-Datei importieren

4. **Browser-Wechsel**:
   - Chrome → Firefox speichert nicht über
   - **Lösung**: Export/Import verwenden

### "Auto-Save funktioniert nicht"

**Debugging-Schritte**:

1. **Browser-Konsole öffnen** (F12):
   ```javascript
   // Prüfe gespeicherte Daten
   localStorage.getItem('gartenplanerDaten');
   localStorage.getItem('beetAnythingState');
   ```

2. **LocalStorage aktiviert?**:
   - Manche Browser blockieren LocalStorage
   - In Inkognito-Modus oft deaktiviert
   - **Lösung**: Normaler Modus, Cookies erlauben

3. **Speicher voll?**:
   - LocalStorage Limit: ~5-10 MB
   - **Lösung**: Alte Daten exportieren & löschen

4. **Browser-Einstellungen**:
   - "Cookies blockieren" deaktiviert LocalStorage
   - **Lösung**: Cookies für diese Seite erlauben

### "Daten werden nicht geladen"

**Check-Liste**:

1. ✅ Gleicher Browser wie beim Speichern?
2. ✅ Gleicher Computer/Gerät?
3. ✅ NICHT im Inkognito-Modus?
4. ✅ Cookies/LocalStorage erlaubt?

**Wenn nichts hilft**:
- Backup importieren
- App neu installieren
- Browser neu starten

---

## 📊 LocalStorage Monitor (für Entwickler)

### Gespeicherte Daten anzeigen:

**Browser-Konsole öffnen** (F12) und eingeben:

```javascript
// Alle Gartenbeete anzeigen
const daten = JSON.parse(localStorage.getItem('gartenplanerDaten'));
console.log('Beete:', daten.beete);
console.log('Pflanzungen:', daten.pflanzungen);

// App-State anzeigen
const state = JSON.parse(localStorage.getItem('beetAnythingState'));
console.log('Jahr:', state.aktuellesJahr);
console.log('Wunschliste:', state.wunschliste);

// Speichergröße prüfen
const size = new Blob([localStorage.getItem('gartenplanerDaten')]).size;
console.log('Datengröße:', (size / 1024).toFixed(2), 'KB');
```

### Manuell speichern (falls nötig):

```javascript
app.speichern();
console.log('Manuell gespeichert!');
```

### Daten manuell löschen:

```javascript
// VORSICHT: Löscht alle Daten!
localStorage.removeItem('gartenplanerDaten');
localStorage.removeItem('beetAnythingState');
location.reload();
```

---

## ✨ Fazit

**Sie müssen sich um nichts kümmern!**

✅ Alles wird automatisch gespeichert  
✅ Beim nächsten Öffnen ist alles da  
✅ Keine manuellen Speicher-Aktionen nötig  
✅ Export/Import nur für Backup oder Geräte-Wechsel  

**Empfehlung für maximale Sicherheit**:
- Einmal pro Monat: Daten exportieren
- Backup in Cloud speichern
- Vor größeren Änderungen: Schnell-Export

---

**Viel Spaß mit Beet Anything - Ihre Gartenpläne sind sicher! 🌱**
