# BEET ANYTHING - Developer Resume v1.2 Pest Protection

## 🎯 Quick Start

**Product Name**: Beet Anything  
**Version**: 1.2 Pest Protection (PWA with Natural Pest Control)  
**File**: `beet-anything.html` (~115 KB)  
**Type**: Single-Page Application (Self-contained)  
**Languages**: English, German, Italian  
**Status**: Production Ready  
**Font**: Inter from https://rsms.me/inter/

---

## 📦 What's Implemented

### Core Features (all ✅)
✅ Multi-year planning with unlimited history  
✅ Dynamic bed management (unlimited)  
✅ **30 trilingual vegetables** with companion planting + pest data  
✅ Intelligent suggestion algorithm (scoring-based)  
✅ Compatibility matrix (30×30 combinations)  
✅ **Pest protection system** (NEW v1.2!)  
✅ **Auto-save after every change** (no manual saving needed!)  
✅ **Auto-load on start** (all data automatically restored)  
✅ Export/import (JSON for backups)  
✅ **PWA installation** (iOS, Android, Desktop)  
✅ **Offline functionality** (Service Worker)  
✅ **Mobile-optimized** (iPhone 16, Android, all devices)  
✅ Responsive design (Desktop, Tablet, Mobile)  
✅ **Internationalization** (EN/DE/IT with language persistence)

### New Features in v1.2 Pest Protection
🆕 **30 vegetables** (up from 20)  
🆕 **Pest profiles** for all vegetables  
🆕 **Protection relationships** (shows which plants protect others)  
🆕 **Vulnerability warnings** (alerts for shared pests)  
🆕 **Beneficial insects** (identifies plants that attract helpers)  
🆕 **Smart pest scoring** (+20/-15 points in algorithm)  
🆕 **Visual pest tags** (🛡️, 🪳, 🐞)  
🆕 **Interactive tooltips** (hover any tag for details)  
🆕 **Individual pest icons** (🐌🦟🐛🪲 per plant)  
🆕 **Slug protection** (14 vulnerable plants, 5 protective plants)  
🆕 **Symbol legend** with hover instructions  
🆕 **Auto-translated bed names** (Bed/Beet/Aiuola)  
🆕 **Data versioning system** (automatic migration v1.0→v1.2)  
🆕 **Clear All Data button** (fresh start option)  
🆕 **15 new translation keys** (tooltips + pest categories + data management)  

---

## 🛡️ Pest Protection System (NEW v1.2!)

### Vegetable Class Extended

```javascript
class Vegetable {
    constructor(id, nameEN, nameDE, nameIT, nutrition, family, pestData = {}) {
        // Existing attributes...
        this.nameEN = nameEN;
        this.nameDE = nameDE;
        this.nameIT = nameIT;
        this.nutrition = nutrition;
        this.family = family;
        
        // NEW: Pest & beneficial data
        this.susceptibleTo = pestData.susceptibleTo || [];
        this.protectsAgainst = pestData.protectsAgainst || [];
        this.attractsBeneficials = pestData.attractsBeneficials || false;
    }
    
    // NEW Methods:
    protectsPlant(otherVegetable) {
        return this.protectsAgainst.some(pest => 
            otherVegetable.susceptibleTo.includes(pest)
        );
    }
    
    sharesVulnerabilitiesWith(otherVegetable) {
        return this.susceptibleTo.filter(pest =>
            otherVegetable.susceptibleTo.includes(pest)
        );
    }
}
```

### Example Pest Data

```javascript
new Vegetable('onion', 'Onion', 'Zwiebel', 'Cipolla', 'medium', 'Amaryllidaceae', {
    susceptibleTo: ['onion-fly', 'thrips'],
    protectsAgainst: ['carrot-fly', 'aphids', 'slugs'],
    attractsBeneficials: false
}),

new Vegetable('basil', 'Basil', 'Basilikum', 'Basilico', 'low', 'Lamiaceae', {
    susceptibleTo: ['aphids', 'japanese-beetle', 'slugs'],
    protectsAgainst: ['aphids', 'whitefly', 'hornworms'],
    attractsBeneficials: true
})
```

### Common Pests in Database

- **aphids** (Blattläuse) - 20+ plants affected
- **slugs** (Schnecken) - 14 plants vulnerable, 5 plants protective
- **flea-beetle** (Erdflöhe) - 6 plants
- **carrot-fly** (Möhrenfliege) - 4 plants
- **cabbage-white** (Kohlweißling) - 5 plants
- **whitefly** (Weiße Fliege) - 2 plants
- Plus 15+ more specific pests

### Protection Examples

| Plant | Protects Against | Protected Plants |
|-------|------------------|------------------|
| **Onion** | carrot-fly, aphids, slugs | Carrot, Lettuce, Strawberry |
| **Garlic** | aphids, slugs, japanese-beetle | Tomato, Strawberry |
| **Chives** | aphids, carrot-fly, slugs, japanese-beetle | Carrot, Tomato, Strawberry |
| **Basil** | aphids, whitefly, hornworms | Tomato, Pepper |
| **Mint** | aphids, cabbage-white, flea-beetle | Cabbage, Tomato |
| **Celery** | cabbage-white | Cabbage, Broccoli |

---

### Tooltip System

**All companion tags have intelligent tooltips:**

```javascript
// Good Companions - shows WHY
✓ Zwiebel
Tooltip: "Traditionell gute Begleitpflanze • Schützt vor: carrot-fly, aphids, slugs"

// Bad Companions - explains incompatibility
✗ Sellerie
Tooltip: "Unverträglich: Konkurriert um Nährstoffe oder hemmt Wachstum"

// Protection - lists specific pests
🛡️ Karotte
Tooltip: "Schützt vor: carrot-fly, aphids"

// Shared Pests - shows vulnerabilities
🪳 Brokkoli
Tooltip: "slugs, cabbage-white, aphids, cabbage-root-fly"

// Beneficials - identifies insects
🐞
Tooltip: "Lockt Nützlinge an: Marienkäfer, Florfliegen, Schlupfwespen, Bestäuber"
```

**Legend with hover instructions:**
- All 5 symbol types explained
- Separate info line: "Detailinformationen sind durch Berühren der jeweiligen Symbole verfügbar"
- Fully translated (EN/DE/IT)

### Individual Pest Icons (NEW!)

**Each plant shows its vulnerabilities with categorized icons:**

```javascript
// 4 pest categories
🐌 Slugs/Snails       → slugs
🦟 Flying pests       → aphids, whitefly, thrips, flies, moths
🐛 Larvae/Caterpillars → cabbage-white, hornworms, wireworms
🪲 Beetles            → potato-beetle, flea-beetle, japanese-beetle

// Example: Lettuce
🥬 Salat (Niedrig)
   Asteraceae
   🐌 🦟 🐛    ← Shows all 3 vulnerabilities

// Example: Tomato
🍅 Tomate (Hoch)
   Solanaceae
   🦟 🐛      ← Shows flying + larvae only
```

**Implementation:**
```javascript
// NEW methods in Vegetable class
getPestIcons() {
    const icons = {slugs: false, flying: false, larvae: false, beetles: false};
    
    const slugPests = ['slugs'];
    const flyingPests = ['aphids', 'whitefly', 'thrips', 'onion-fly', 'carrot-fly', ...];
    const larvaePests = ['cabbage-white', 'hornworms', 'wireworms', ...];
    const beetlePests = ['potato-beetle', 'flea-beetle', 'japanese-beetle', ...];
    
    for (const pest of this.susceptibleTo) {
        if (slugPests.includes(pest)) icons.slugs = true;
        if (flyingPests.includes(pest)) icons.flying = true;
        if (larvaePests.includes(pest)) icons.larvae = true;
        if (beetlePests.includes(pest)) icons.beetles = true;
    }
    
    return icons;
}

getPestsByCategory() {
    // Returns: {slugs: ['slugs'], flying: ['aphids', 'whitefly'], ...}
}

// Usage in UI
const pestIcons = veg.getPestIcons();
const pestsByCategory = veg.getPestsByCategory();

if (pestIcons.slugs) {
    const tooltip = this.t('tooltip.slugs') + ': ' + pestsByCategory.slugs.join(', ');
    html += `<span class="pest-icon" title="${tooltip}">🐌</span>`;
}
```

**CSS for pest icons:**
```css
.pest-icons {
    display: flex;
    gap: 0.35rem;
    margin-top: 0.5rem;
}

.pest-icon {
    font-size: 1.1rem;
    cursor: help;
    opacity: 0.8;
    transition: opacity 0.2s ease, transform 0.2s ease;
}

.pest-icon:hover {
    opacity: 1;
    transform: scale(1.15);
}
```

**Tooltips show specific pests:**
- Hover 🐌: "Schnecken: slugs"
- Hover 🦟: "Fliegende Schädlinge (Blattläuse, Fliegen, Motten): aphids, whitefly"
- Hover 🐛: "Larven/Raupen: cabbage-white, hornworms"
- Hover 🪲: "Käfer: flea-beetle, potato-beetle"

### Auto-Translated Bed Names (NEW!)

**Default bed names translate automatically:**

```javascript
class GardenBed {
    constructor(id, name) {
        this.id = id;
        this.name = name;
    }
    
    getName(lang) {
        // Check if this is a default name pattern
        const defaultPatterns = [
            /^Bed (\d+)$/,      // English
            /^Beet (\d+)$/,     // German
            /^Aiuola (\d+)$/    // Italian
        ];
        
        for (const pattern of defaultPatterns) {
            const match = this.name.match(pattern);
            if (match) {
                const number = match[1];
                const translations = {
                    en: `Bed ${number}`,
                    de: `Beet ${number}`,
                    it: `Aiuola ${number}`
                };
                return translations[lang] || this.name;
            }
        }
        
        // Not a default name, return as-is (user-defined)
        return this.name;
    }
}

// Usage in render
${bed.getName(this.currentLanguage)}  // Auto-translates!
```

**Examples:**
- EN: "Bed 1, Bed 2, Bed 3"
- DE: "Beet 1, Beet 2, Beet 3"
- IT: "Aiuola 1, Aiuola 2, Aiuola 3"

**User-defined names:**
- "Nordseite" → stays "Nordseite" in all languages
- "Sunny Corner" → stays "Sunny Corner" in all languages

**How it works:**
1. User creates bed → saved as "Bed 1" (English default)
2. Switch to German → displays "Beet 1"
3. Switch to Italian → displays "Aiuola 1"
4. User renames to "Terrasse" → stays "Terrasse" in all languages
5. Switch back to English → still shows "Terrasse" (user-defined)

### Data Versioning & Migration (NEW!)

**Problem solved:** Old data from v1.0 works seamlessly with v1.2

**Version system:**
```javascript
{
  "version": "1.2",  // NEW: Every export includes version
  "vegetables": [...],
  "beds": [...],
  "plantings": [...]
}
```

**Automatic migration:**
```javascript
migrateData(data) {
    const currentVersion = '1.2';
    const dataVersion = data.version || '1.0';
    
    console.log(`Migrating data from v${dataVersion} to v${currentVersion}`);
    
    // v1.0 → v1.1: Add pest data
    if (!data.version || data.version === '1.0') {
        console.log('Migrating from v1.0: Adding pest data to vegetables');
        
        data.vegetables = data.vegetables.map(veg => {
            // Add empty pest arrays if missing
            if (!veg.susceptibleTo) veg.susceptibleTo = [];
            if (!veg.protectsAgainst) veg.protectsAgainst = [];
            if (veg.attractsBeneficials === undefined) 
                veg.attractsBeneficials = false;
            return veg;
        });
        
        data.version = '1.1';
    }
    
    // v1.1 → v1.2: Future migrations
    if (data.version === '1.1') {
        console.log('Migrating from v1.1 to v1.2');
        // Add new features here when needed
        data.version = '1.2';
    }
    
    return data;
}
```

**Console output:**
```
✅ Loaded data version: 1.2
```

or during migration:
```
Migrating data from v1.0 to v1.2
Migrating from v1.0: Adding pest data to vegetables
Data successfully imported (version 1.2)
```

**Clear All Data feature:**
```javascript
clearAllData() {
    const confirmed = confirm(this.t('data.clearConfirm'));
    if (confirmed) {
        localStorage.removeItem('beetAnythingData');
        localStorage.removeItem('beetAnythingState');
        alert(this.t('data.cleared'));
        window.location.reload();
    }
}
```

**UI Button:**
- Header: 🗑️ Clear All Data
- Confirmation required
- Translated in EN/DE/IT
- Complete reset with page reload

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

**File Location**: `SuggestionEngine.scorePlantingOption()` (approx. line 1764)

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
| **Pest protection** | **+20** | **Protects other plants (NEW!)** |
| **Shared pests** | **-15** | **Plants share vulnerabilities (NEW!)** |
| **Beneficial insects** | **+10** | **Attracts helpers (NEW!)** |
| Empty bed | +5 | No current plants |
| 2-year rotation | -10 | Same plant 2 years ago |

**Output**: Sorted list with bed-vegetable assignments + reasons

### Example Scores:

**Tomato + Basil in same bed:**
- Good companion: +15
- Basil protects tomato: +20
- Basil attracts beneficials: +10
- **Total bonus: +45 points!** 🌟

**Cabbage + Broccoli (BAD!):**
- Same family: -20
- Share pests (cabbage-white, aphids): -15
- Both heavy feeders: -15
- **Total penalty: -50 points!** ⚠️

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

### 1. Add New Vegetable (with Pest Data)

**Location**: `GardenManager.initializeVegetableDatabase()` (approx. line 1406)

```javascript
// Step 1: Create vegetable with pest data
const veggies = [
    // ... existing ...
    new Vegetable('beetroot', 'Beetroot', 'Rote Beete', 'Barbabietola', 'medium', 'Amaranthaceae', {
        susceptibleTo: ['aphids', 'leaf-miners'],
        protectsAgainst: [],
        attractsBeneficials: false
    }),
];

// Step 2: Set companions
this.setCompanions('beetroot',
    ['onion', 'cabbage'],     // Good companions
    ['spinach', 'leek']        // Bad companions
);
```

### 2. Add New Pest Type

Just add to the relevant vegetable's `susceptibleTo` or `protectsAgainst` arrays:

```javascript
new Vegetable('tomato', 'Tomato', 'Tomate', 'Pomodoro', 'high', 'Solanaceae', {
    susceptibleTo: ['aphids', 'whitefly', 'hornworms', 'blight'],  // Added 'blight'
    protectsAgainst: [],
    attractsBeneficials: false
}),
```

### 3. Add New Language

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
        // ... all ~65 keys (including pest reasons)
        "reason.pestProtection": "🛡️ Protège contre les parasites",
        "reason.sharedPestRisk": "⚠️ Attire les mêmes parasites que",
        "reason.attractsBeneficials": "🐞 Attire les insectes bénéfiques",
    }
};

// Update Vegetable class:
class Vegetable {
    constructor(id, nameEN, nameDE, nameIT, nameFR, nutrition, family, pestData) {
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
| **Pest translations** | **~1108** | **Pest reason keys (NEW!)** |
| Vegetable database | ~1406 | `initializeVegetableDatabase()` |
| **Pest data** | **~1409** | **Vegetable + pestData (NEW!)** |
| Companion rules | ~1470 | `setCompanions()` calls |
| Scoring algorithm | ~1764 | `scorePlantingOption()` |
| **Pest scoring** | **~1820** | **Pest protection logic (NEW!)** |
| Auto-save logic | ~2300 | `app.save()` |
| Auto-load logic | ~1836 | `app.init()` |
| UI rendering | ~2308 | `app.render()` |
| **Pest UI tags** | **~2340** | **Protection/warning tags (NEW!)** |
| PWA install code | ~2400 | Service Worker + install buttons |
| Export/import | ~2250 | `exportData()` / `importData()` |
| Language switch | ~1875 | `setLanguage()` |

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

1. **Open file**: `beet-anything.html` in editor
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
git add beet-anything.html
# Rename to index.html!
mv beet-anything.html index.html
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
**Version**: 1.2 Pest Protection  
**Status**: Production Ready  
**Developed for**: Private vegetable gardeners  
**Maintenance**: Self-contained, no dependencies (except Inter Font)  
**GitHub**: https://github.com/schatzl/beet-anything
