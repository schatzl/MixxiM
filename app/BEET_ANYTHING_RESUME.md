# BEET ANYTHING - Developer Resume v1.1 i18n

## 🎯 Quick Start

**Product Name**: Beet Anything  
**Version**: 1.1 i18n (Internationalized Progressive Web App)  
**File**: `beet-anything-i18n.html` (~105 KB)  
**Type**: Single-Page Application (Self-contained)  
**Languages**: English, German, Italian  
**Status**: Production Ready  
**Font**: Inter from https://rsms.me/inter/

---

## 📦 What's Implemented

### Core Features (all ✅)
✅ Multi-year planning with unlimited history  
✅ Dynamic bed management (unlimited)  
✅ 20 trilingual vegetables with companion planting data  
✅ Intelligent suggestion algorithm (scoring-based)  
✅ Compatibility matrix (20×20 combinations)  
✅ **Auto-save after every change** (no manual saving needed!)  
✅ **Auto-load on start** (all data automatically restored)  
✅ Export/import (JSON for backups)  
✅ **PWA installation** (iOS, Android, Desktop)  
✅ **Offline functionality** (Service Worker)  
✅ **Mobile-optimized** (iPhone 16, Android, all devices)  
✅ Responsive design (Desktop, Tablet, Mobile)  
✅ **Internationalization** (EN/DE/IT with language persistence)

### New Features in v1.1 i18n
🆕 **Trilingual support** (English, German, Italian)  
🆕 **Language persistence** (remembers language choice)  
🆕 **All vegetable names translated** (20 vegetables × 3 languages)  
🆕 **Complete UI translation** (~60 strings per language)  
🆕 **Language switch in header** (instant switching)  

---

## 🏗️ Architecture Overview

### Classes (OOP Hierarchy)

```
Vegetable              → Vegetable data + companion logic
GardenBed              → Bed metadata
Planting               → Bed-year-vegetable linking
GardenManager          → Central data management
SuggestionEngine       → Algorithm for optimal assignment
app (Global)           → UI controller + event handlers
```

### Data Flow

```
User Interaction
    ↓
app.* Methods (Controller)
    ↓
GardenManager (Model)
    ↓
app.save() → LocalStorage (AUTO!)
    ↓
app.render() (View)
    ↓
DOM Update
```

---

## 🌍 Internationalization System

### Translation Object

```javascript
const translations = {
    en: {
        "btn.export": "💾 Export Data",
        "wishlist.title": "Your Wishlist",
        // ... ~60 keys
    },
    de: {
        "btn.export": "💾 Daten exportieren",
        "wishlist.title": "Ihre Wunschliste",
        // ... ~60 keys
    },
    it: {
        "btn.export": "💾 Esporta dati",
        "wishlist.title": "La tua lista dei desideri",
        // ... ~60 keys
    }
};
```

### Vegetable Names (Multilingual)

```javascript
class Vegetable {
    constructor(id, nameEN, nameDE, nameIT, nutrition, family) {
        this.nameEN = nameEN;  // English
        this.nameDE = nameDE;  // German
        this.nameIT = nameIT;  // Italian
    }
    
    getName(lang = 'en') {
        if (lang === 'de') return this.nameDE;
        if (lang === 'it') return this.nameIT;
        return this.nameEN;
    }
}

// Example:
new Vegetable('tomato', 'Tomato', 'Tomate', 'Pomodoro', 'high', 'Solanaceae')
```

### Language Switch

**HTML:**
```html
<div class="language-switch">
    <button onclick="app.setLanguage('en')" id="langEN">EN</button>
    <button onclick="app.setLanguage('de')" id="langDE">DE</button>
    <button onclick="app.setLanguage('it')" id="langIT">IT</button>
</div>
```

**Usage in HTML:**
```html
<button data-i18n="btn.export">💾 Export Data</button>
```

**Usage in JavaScript:**
```javascript
app.t('btn.export') // Returns translated string
```

### Language Persistence

```javascript
// Saved automatically:
localStorage.setItem('beetAnythingState', JSON.stringify({
    currentYear: 2024,
    wishlist: ['tomato', 'carrot'],
    language: 'it'  // ← Persisted!
}));

// Loaded on startup:
this.currentLanguage = parsedState.language || 'en';
```

---

## 🔄 Auto-Save System (IMPORTANT!)

### Automatically Saved After:

| Action | Saved |
|--------|-------|
| Add bed | ✅ Immediately |
| Remove bed | ✅ Immediately |
| Rename bed | ✅ On modal save |
| Add plant | ✅ Immediately |
| Remove plant | ✅ Immediately |
| Change year | ✅ Immediately |
| Change wishlist | ✅ Immediately |
| Apply suggestion | ✅ Immediately |
| Change language | ✅ Immediately |

**NO manual saving needed!** Everything automatic.

### LocalStorage Keys

```javascript
'beetAnythingData'     // Main data (beds, plantings, vegetables)
'beetAnythingState'    // App state (year, wishlist, language)
```

### Most Important App Methods

```javascript
app.init()                          // Initialization + auto-load
app.save()                          // Auto-save (called automatically!)
app.setLanguage(lang, save)        // Change language + save
app.changeYear(±1)                 // Navigate year + auto-save
app.generateSuggestions()          // Start algorithm
app.openBedModal(bedId)            // Edit bed
app.exportData()                   // JSON download (manual backup)
app.importData()                   // JSON upload (restore)
app.showMatrix()                   // Companion planting matrix
app.installAsApp()                 // Trigger PWA installation
app.render()                       // Update UI
```

---

## 📱 PWA Features

### Detect Installation

```javascript
// App checks automatically:
if (window.matchMedia('(display-mode: standalone)').matches) {
    // App is running as PWA
    // Install buttons are hidden
}
```

### Install Button Positions

1. **Header Button** (ID: `headerInstallButton`)
   - Always visible (except when installed)
   - At "📱 Install as App"
   - Works on all devices

2. **Floating Button** (ID: `floatingInstallButton`)
   - Bottom right (desktop)
   - Full width bottom (mobile)
   - Only when browser supports PWA

### Check Installation Status

**In Browser DevTools Console:**
```javascript
// Check if installed as PWA:
window.matchMedia('(display-mode: standalone)').matches

// If true → App is installed
// If false → App runs in browser
```

**Visual Indicators:**
- ✅ Install button gone = App is installed
- ✅ No browser bar = Running as PWA
- ✅ App icon on homescreen = Installed

### Service Worker

**Cached:**
- App shell (HTML, CSS, JS)
- Fonts (Inter from rsms.me)

**Available Offline:**
- All features (planning, editing, algorithm)
- LocalStorage works offline
- Only first installation needs internet

---

## 🧮 Algorithm Core Logic

**File Location**: `SuggestionEngine.scorePlantingOption()` (approx. line 1500)

### Scoring Weights:

| Criterion | Points | Condition |
|-----------|--------|-----------|
| Family rotation | +30 | Different family than previous year |
| Family rotation | -20 | Same family as previous year |
| Nutrition rotation | +25 | Light feeder after heavy feeder |
| Nutrition rotation | -15 | Heavy feeder after heavy feeder |
| Nutrition rotation | +10 | Light feeder generally |
| Good companion | +15 | Per compatible plant |
| Bad companion | -30 | Per incompatible plant |
| Empty bed | +5 | No current plants |
| 2-year rotation | -10 | Same plant 2 years ago |

**Output**: Sorted list with bed-vegetable assignments + reasons

---

## 📊 Data Structure

### LocalStorage

```javascript
// Main data
localStorage.getItem('beetAnythingData')
{
  "vegetables": [...],  // 20 vegetables
  "beds": [...],        // All beds
  "plantings": [...]    // All plantings (all years)
}

// App state
localStorage.getItem('beetAnythingState')
{
  "currentYear": 2024,
  "wishlist": ["tomato", "carrot"],
  "language": "en"
}
```

---

## 🎨 Design System

### Font: Inter (rsms.me)

```css
@import url('https://rsms.me/inter/inter.css');

font-family: 'Inter', sans-serif;
font-feature-settings: 'liga' 1, 'calt' 1;
```

**Weights:**
- 400 (Normal): Body text
- 700 (Bold): h2, h3
- 800 (Extra Bold): h1

### CSS Variables (Color Scheme)

```css
--soil-dark: #3a2f28      /* Primary text */
--leaf-green: #4a7c59     /* Primary color */
--sage: #8ba888           /* Secondary color */
--cream: #f4f1ea          /* Background */
--terracotta: #c1694f     /* Accent/heavy feeder */
--sun-yellow: #e8b84d     /* Highlight/medium feeder */
```

### Responsive Breakpoints

| Breakpoint | Layout |
|------------|--------|
| > 968px | 2-column (1:2) |
| 768-968px | 1-column |
| 480-768px | 1-column, compact |
| 375-480px | 1-column, mobile |
| < 375px | 1-column, minimal |

**Landscape < 968px**: 2-column (1:1.5)

---

## 🔧 Common Customizations

### 1. Add New Vegetable

**Location**: `GardenManager.initializeVegetableDatabase()` (approx. line 1320)

```javascript
// Step 1: Create vegetable
const veggies = [
    // ... existing ...
    new Vegetable('arugula', 'Arugula', 'Rucola', 'Rucola', 'low', 'Brassicaceae'),
];

// Step 2: Set companions
this.setCompanions('arugula',
    ['beans', 'peas'],     // Good companions
    []                      // Bad companions
);
```

### 2. Add New Language

**Location**: `translations` object (approx. line 1013)

```javascript
const translations = {
    en: { ... },
    de: { ... },
    it: { ... },
    fr: {  // New: French
        title: "Beet Anything",
        subtitle: "Rotation des cultures facile",
        "btn.export": "💾 Exporter",
        // ... all ~60 keys
    }
};

// Update Vegetable class:
class Vegetable {
    constructor(id, nameEN, nameDE, nameIT, nameFR, nutrition, family) {
        this.nameFR = nameFR;  // Add French
    }
    
    getName(lang = 'en') {
        if (lang === 'fr') return this.nameFR;  // Add French
        // ...
    }
}

// Update HTML:
<button onclick="app.setLanguage('fr')" id="langFR">FR</button>
```

### 3. Change Scoring Weights

**Location**: `SuggestionEngine.scorePlantingOption()` (approx. line 1500)

```javascript
// Increase family rotation importance
score += 50;  // instead of 30

// Stricter bad companion penalty
score -= 50;  // instead of 30
```

### 4. Add New Scoring Criteria

```javascript
// Example: Sun requirement
if (veg.sunRequirement === 'full' && bed.sunny) {
    score += 20;
    reasons.push('reason.optimalSun');
}
```

### 5. Change Color Scheme

```css
:root {
    --leaf-green: #2d5f3f;  /* Darker */
    --cream: #ffffff;        /* Whiter */
}
```

---

## 🐛 Debugging Tips

### Check LocalStorage

```javascript
// Browser console:
localStorage.getItem('beetAnythingData')
localStorage.getItem('beetAnythingState')

// Check size
const size = new Blob([localStorage.getItem('beetAnythingData')]).size;
console.log('Size:', (size / 1024).toFixed(2), 'KB');
```

### Reset Data

```javascript
// CAUTION: Deletes all data!
localStorage.removeItem('beetAnythingData');
localStorage.removeItem('beetAnythingState');
location.reload();
```

### Check PWA Installation

```javascript
// Running as PWA?
window.matchMedia('(display-mode: standalone)').matches

// Install prompt available?
window.deferredPrompt !== null
```

### Test Auto-Save

```javascript
// Manually trigger
app.save();

// View saved data
console.log(JSON.parse(localStorage.getItem('beetAnythingState')));
```

### Test Language System

```javascript
// Change language
app.setLanguage('it');

// Get translation
app.t('btn.export');  // "💾 Esporta dati"

// Get vegetable name
const tomato = app.garden.vegetables.get('tomato');
tomato.getName('it');  // "Pomodoro"
```

---

## 📝 Code Conventions

### Naming (English)

```javascript
// Variables: camelCase
currentYear, wishlist, bedId

// Classes: PascalCase
Vegetable, GardenBed, SuggestionEngine

// Methods: camelCase + Verb
addBed(), generateSuggestions()

// CSS classes: kebab-case
.bed-header, .plant-assignment, .nutrition-badge
```

---

## 🔍 Important File Locations

### Line Reference (approximate)

| Feature | Line | Description |
|---------|------|-------------|
| Translations | ~1013 | `translations` object (EN/DE/IT) |
| Vegetable database | ~1320 | `initializeVegetableDatabase()` |
| Companion rules | ~1345 | `setCompanions()` calls |
| Scoring algorithm | ~1500 | `scorePlantingOption()` |
| Auto-save logic | ~2040 | `app.save()` |
| Auto-load logic | ~1598 | `app.init()` |
| UI rendering | ~1900 | `app.render()` |
| PWA install code | ~2130 | Service Worker + install buttons |
| Export/import | ~1990 | `exportData()` / `importData()` |
| Language switch | ~1637 | `setLanguage()` |

---

## 🚀 Next Development Steps

### Priority 1 (Quick Wins)
- [ ] More vegetables (goal: 30-40)
- [ ] Sowing/harvest calendar
- [ ] Print function for yearly plan
- [ ] Notes field per bed
- [ ] Dark mode
- [ ] French translation (FR)

### Priority 2 (Medium)
- [ ] Bed size input
- [ ] Area calculation
- [ ] Plant spacing
- [ ] Images/photos per vegetable
- [ ] Statistics (harvest quantities)

### Priority 3 (Advanced)
- [ ] Graphical bed visualization (SVG/Canvas)
- [ ] Drag & drop between beds
- [ ] User-defined companion rules
- [ ] Cloud sync (optional)
- [ ] Native mobile app

---

## 📱 Mobile Testing

### Browser DevTools

**Chrome/Edge**:
```
1. F12 → DevTools
2. Toggle device toolbar (Ctrl+Shift+M)
3. Device: iPhone 16 Pro (393x852)
4. Test!
```

**Firefox**:
```
1. F12 → DevTools
2. Responsive Design Mode (Ctrl+Shift+M)
3. Viewport: 393x852
4. Test!
```

### Real Device

**iPhone**:
1. Host file on Netlify/GitHub Pages
2. Open URL in Safari
3. Share (□↑) → "Add to Home Screen"
4. Test as PWA

**Android**:
1. Host file
2. Open URL in Chrome
3. Click "Install as App"
4. Test as PWA

---

## 💾 Backup Strategy

### For Developers
1. Use Git repository
2. Regular commits
3. Tags per version (v1.0, v1.1, etc.)

### For Users
1. **Automatic**: LocalStorage (persists)
2. **Manual**: Monthly export recommended
3. **Cloud**: Backup to Dropbox/Google Drive

### Export Filenames
```
garden-plan-2025-02-03.json
gartenplan-2025-02-03.json   (DE)
piano-giardino-2025-02-03.json   (IT)
```
(Automatic timestamp)

---

## ⚠️ Known Limitations

### Functional
1. **No seasons**: Only annual planning, no early/late crops
2. **No areas**: Bed size not considered
3. **Static rules**: Companion planting hard-coded
4. **Single-user**: No collaboration

### Technical
1. **LocalStorage limit**: ~5-10 MB
2. **No cloud sync**: Data stays on device
3. **Browser-specific**: PWA installation not everywhere

---

## 🆘 Common Problems

### "Auto-save doesn't work"

**Check:**
```javascript
// LocalStorage enabled?
typeof(Storage) !== "undefined"

// Incognito mode?
// → No LocalStorage available

// Storage full?
// → Export old data & delete
```

### "Data is gone"

**Causes:**
- Cache cleared (with "cookies and website data")
- Different browser/device
- Incognito mode used

**Solution:**
- Import backup file
- Future: Export regularly

### "Install button doesn't appear"

**Check:**
```javascript
// Already installed?
window.matchMedia('(display-mode: standalone)').matches

// Browser supports PWA?
// iOS: Only Safari
// Android: Chrome, Edge, Samsung Internet
// Desktop: Chrome, Edge, Opera
```

### "App doesn't work offline"

**Solution:**
- Open with internet at least once
- Service Worker must be registered
- Cache is filled on first visit

### "Language doesn't persist"

**Check:**
```javascript
// Check saved state:
JSON.parse(localStorage.getItem('beetAnythingState'))

// Should contain:
{ language: 'de', currentYear: 2024, wishlist: [...] }
```

---

## 📈 Performance Tips

### Optimize for Many Beds (>50)

```javascript
// For >100 beds: Optimize rendering
// Only render visible beds (Virtual Scrolling)

// For >1000 plantings: Indexing
// Map-based lookups instead of array filter
```

### Reduce LocalStorage Size

```javascript
// Archive old years
// Export years < 2020 to separate JSON
// Remove from LocalStorage
```

---

## ✅ Pre-Release Checklist

Before each new version:

- [ ] Manually test all features
- [ ] Test auto-save/load (5 scenarios)
- [ ] Export/import with sample data
- [ ] Browser compatibility (Chrome, Firefox, Safari)
- [ ] Mobile view test (iPhone, Android)
- [ ] PWA installation test
- [ ] Offline mode test
- [ ] LocalStorage limits test (>100 beds)
- [ ] All 3 languages working
- [ ] Language persistence working
- [ ] Update code comments
- [ ] Change version number in documentation
- [ ] Update CHANGELOG
- [ ] Update README

---

## 🎓 For New Developers

### Get Started in 5 Minutes

1. **Open file**: `beet-anything-i18n.html` in editor
2. **Search concept**: Ctrl+F "Vegetable" → Find class
3. **Understand**: OOP hierarchy → GardenManager → SuggestionEngine
4. **Customize**: Add vegetable (see above)
5. **Test**: Open file in browser

### Most Important Concepts

1. **Class hierarchy**: Vegetable, GardenBed, Planting
2. **Maps instead of arrays**: Faster lookups
3. **Auto-save system**: After every change
4. **Scoring algorithm**: Multiple criteria combined
5. **PWA**: Service Worker + Manifest
6. **i18n**: Translation object + multilingual data

### Code Style

- **English for everything**: Variables, classes, methods, comments
- **Translation system**: For UI strings
- **Comments**: Where needed, not everywhere
- **Structure**: Classes → Manager → App → UI

---

## 📞 Support Resources

### Documentation

1. **BEET_ANYTHING_SPECIFICATION.md** - Complete
2. **This Resume** - Quick reference
3. **APP_INSTALLATION_GUIDE.md** - PWA installation
4. **MOBILE_OPTIMIZATION.md** - Responsive design
5. **README.md** - Project overview

### In Code

- JSDoc comments for classes
- Inline comments for complex logic
- Dividers between code sections

---

## 🔐 Security

### No Risks
- No server contact
- No API calls
- No cookies/tracking
- No passwords

### Best Practices
- JSON.parse in try-catch
- Input validation on import
- No eval() used
- No external scripts (except Inter Font)

---

## 🏁 Deployment

### Option 1: Static File
```bash
# Simply upload to web server
# Works immediately, no build needed
```

### Option 2: GitHub Pages
```bash
git init
git add beet-anything-i18n.html
# Rename to index.html!
mv beet-anything-i18n.html index.html
git commit -m "Initial commit"
git push origin main
# → Enable GitHub Pages
# URL: https://username.github.io/repo-name
```

### Option 3: Netlify
```bash
# Drag & drop to Netlify
# Upload file as index.html
# Automatic HTTPS
# URL: https://beet-anything.netlify.app
```

---

## 📊 Metrics (Typical Usage)

| Metric | Value |
|--------|-------|
| File size (HTML) | ~105 KB |
| File size (Minified) | ~50 KB |
| File size (Gzip) | ~25 KB |
| LocalStorage (10 beds, 3 years) | ~20 KB |
| LocalStorage (50 beds, 10 years) | ~100 KB |
| Load time (WiFi) | < 1s |
| Load time (4G) | < 2s |
| Load time (Cached) | < 0.5s |

---

**Last Updated**: February 2025  
**Version**: 1.1 i18n  
**Status**: Production Ready  
**Developed for**: Private vegetable gardeners  
**Maintenance**: Self-contained, no dependencies (except Inter Font)
