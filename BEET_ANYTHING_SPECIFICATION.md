# Beet Anything - Product Specification v1.2 Pest Protection

## Product Overview

**Product Name:** Beet Anything  
**Version:** 1.2 Pest Protection (Progressive Web App with Natural Pest Control)  
**Type:** Web-based garden planning application with app installation  
**Purpose:** Intelligent planning of vegetable gardens considering crop rotation, companion planting, and natural pest protection  
**Platforms:** Web, iOS (Safari), Android (Chrome), Desktop (all browsers)  
**Languages:** English, German, Italian (extensible)

## Core Functionality

### 1. Multi-Year Planning
- Navigation between different years (Forward/Backward)
- Historical planting data for each bed and year
- Display of previous year's plantings for better planning
- Unlimited year history (limited only by storage space)

### 2. Bed Management
- Dynamic adding/removing of garden beds
- Individual naming of each bed
- Assignment of multiple plants per bed and year
- Visual representation of current and past plantings
- Unlimited number of beds possible

### 3. Vegetable Database
Currently 30 vegetable varieties with the following attributes:

#### Included Vegetables:

**Original 20:**
- Tomato, Potato, Carrot, Lettuce, Cabbage
- Beans, Peas, Onion, Garlic
- Cucumber, Zucchini, Corn, Radish
- Spinach, Basil, Pepper, Celery
- Arugula, Kohlrabi, Leek

**New in v1.2:**
- Broccoli, Chives, Parsley, Pumpkin, Mint
- Strawberry, Turnip, Rhubarb, Eggplant, Fennel

#### Attributes per Vegetable:
- **ID**: Unique identifier (lowercase, e.g., "tomato")
- **Names**: English, German, Italian (nameEN, nameDE, nameIT)
- **Nutrition Demand**: high / medium / low
- **Plant Family**: Botanical family (e.g., Solanaceae)
- **Good Companions**: Array of compatible plant IDs
- **Bad Companions**: Array of incompatible plant IDs
- **Susceptible To**: Array of pests this plant attracts (NEW v1.2)
- **Protects Against**: Array of pests this plant repels (NEW v1.2)
- **Attracts Beneficials**: Boolean - attracts helpful insects (NEW v1.2)

### 4. Wishlist System
- Selection of desired vegetables for the current year
- Easy adding/removing of vegetables
- Visual tag-based display
- Automatic saving of wishlist

### 5. Intelligent Suggestion Algorithm

#### Scoring Criteria (Scoring System):

**A. Family Rotation (±30 points)**
- +30: Different plant family than previous year
- -20: Same plant family as previous year
- Prevents soil fatigue and pest accumulation

**B. Nutrition Rotation (±25 points)**
- +25: Light feeder after heavy feeder (optimal for soil regeneration)
- +10: Light feeder generally (soil-friendly)
- -15: Heavy feeder after heavy feeder (soil stress)

**C. Companion Planting Compatibility (±30 points)**
- +15: Per good companion in the same bed (synergies)
- -30: Per bad companion in the same bed (competition/allelopathy)

**D. Pest Protection (±20 points)** *NEW in v1.2!*
- +20: Plant protects others from pests (natural pest control)
- -15: Plants share pest vulnerabilities (increased risk)
- +10: Attracts beneficial insects (ladybugs, lacewings, parasitic wasps)

**E. Additional Factors**
- +5: Empty bed (more flexibility for planning)
- -10: Same plant 2 years ago (extended rotation)

#### Algorithm Flow:
1. Calculate score for each vegetable-bed combination
2. Sort by score (descending)
3. Assign vegetables one by one to the best available bed
4. Avoid double assignments (each vegetable only once, each bed only once)
5. Generate reasons for each recommendation

### 6. Compatibility Matrix
- Tabular overview of all companion planting relationships
- Shows all 20×20 combinations
- Color coding:
  - ✓ Green = Good companions (mutually beneficial)
  - ✗ Red = Bad companions (mutually inhibiting)
  - ○ Gray = Neutral (no known interactions)
- Scrollable view for large datasets
- Sticky header (remains visible when scrolling)

### 7. Data Persistence

#### A. Automatic Saving (LocalStorage)
**Saved after every action:**
- Add/remove/rename bed
- Add/remove plant to bed
- Change year
- Change wishlist
- Apply suggestion

**Two LocalStorage keys:**
1. `beetAnythingData` - Main data (vegetables, beds, plantings)
2. `beetAnythingState` - App state (year, wishlist, language)

**Automatic Loading:**
- All data is restored on app start
- No manual action required
- Preserves complete history

#### B. Manual Export/Import (JSON)
- **Export**: Download as JSON file with timestamp
- **Import**: Upload JSON files
- **Use**: Backups, device changes, sharing with others
- **Data Structure**: Complete JSON with all vegetables, beds, plantings

### 8. Progressive Web App (PWA) Features

#### Installation
- **iOS (Safari)**: "Add to Home Screen" via Share menu
- **Android (Chrome)**: Automatic install prompt or menu
- **Desktop**: Browser install prompt (Chrome, Edge, Opera)

#### Install Button Positions:
1. **Header Button**: Always visible at "📱 Install as App"
2. **Floating Button**: Bottom right (only if browser supports PWA)

#### Behavior After Installation:
- ✅ Fullscreen mode (no browser bar)
- ✅ App icon on homescreen/desktop
- ✅ Faster startup (from cache)
- ✅ Offline functionality
- ✅ App appears in app switcher
- ✅ Install buttons are hidden

#### Offline Functionality
- **Service Worker**: Cached app shell
- **All features available offline**: Planning, editing, algorithm
- **LocalStorage**: Works offline
- **Only needed for first installation**: Internet connection

#### Detect Installation:
```javascript
// App automatically checks if installed as PWA:
if (window.matchMedia('(display-mode: standalone)').matches) {
    // Install buttons are hidden
    // App is running as PWA
}
```

**Visible Indicators:**
- Install button disappears after installation
- Browser bar missing in fullscreen mode
- App icon present on homescreen/desktop

### 9. Internationalization (i18n)

#### Supported Languages:
- **English (EN)**: Default language
- **German (DE)**: Vollständige deutsche Übersetzung
- **Italian (IT)**: Traduzione completa in italiano

#### Language Switch:
- UI element in header (top right)
- Three buttons: EN | DE | IT
- Instant switching without page reload
- All UI elements update immediately

#### What Gets Translated:
- All buttons and labels
- Form fields and placeholders
- Modal dialogs
- Suggestion reasons
- Vegetable names
- Info texts and instructions
- Installation guides

#### Language Persistence:
```javascript
// Language stored in LocalStorage:
localStorage.setItem('beetAnythingState', JSON.stringify({
    language: 'it',
    currentYear: 2024,
    wishlist: [...]
}));

// Restored on next visit:
this.currentLanguage = parsedState.language || 'en';
```

#### Translation System:
```javascript
const translations = {
    en: { "btn.export": "💾 Export Data" },
    de: { "btn.export": "💾 Daten exportieren" },
    it: { "btn.export": "💾 Esporta dati" }
};

// Usage in HTML:
<button data-i18n="btn.export">💾 Export Data</button>

// Usage in JavaScript:
app.t('btn.export') // Returns translated string
```

---

## Technical Architecture

### Class Hierarchy

```
Vegetable
├── id: string
├── nameEN: string
├── nameDE: string
├── nameIT: string
├── nutrition: 'high' | 'medium' | 'low'
├── family: string
├── goodCompanions: string[]
├── badCompanions: string[]
├── susceptibleTo: string[]              (NEW v1.2)
├── protectsAgainst: string[]            (NEW v1.2)
├── attractsBeneficials: boolean         (NEW v1.2)
└── Methods:
    ├── addGoodCompanion(id)
    ├── addBadCompanion(id)
    ├── isCompatibleWith(id): -1 | 0 | 1
    ├── protectsPlant(other): boolean         (NEW v1.2)
    ├── sharesVulnerabilitiesWith(other)      (NEW v1.2)
    ├── getPestIcons(): object                (NEW v1.2: returns {slugs, flying, larvae, beetles})
    ├── getPestsByCategory(): object          (NEW v1.2: categorized pest lists)
    ├── getName(lang): string
    ├── toJSON()
    └── fromJSON(data)

GardenBed
├── id: number (timestamp)
├── name: string
└── Methods:
    ├── getName(lang) → string (NEW v1.2: translates default names)
    ├── toJSON()
    └── fromJSON(data)

Planting
├── bedId: number
├── year: number
├── vegetableId: string
└── Methods:
    ├── toJSON()
    └── fromJSON(data)

GardenManager
├── vegetables: Map<string, Vegetable>
├── beds: Map<number, GardenBed>
├── plantings: Planting[]
└── Methods:
    ├── initializeVegetableDatabase()
    ├── setCompanions(id, good[], bad[])
    ├── addBed(name)
    ├── removeBed(id)
    ├── addPlanting(bedId, year, vegetableId)
    ├── removePlanting(bedId, year, vegetableId)
    ├── getPlantingsForBed(bedId, year)
    ├── getPlantingIdsForBed(bedId, year)
    ├── exportData(): JSON
    ├── importData(json): boolean
    ├── saveToLocalStorage()
    └── loadFromLocalStorage(): boolean

SuggestionEngine
├── garden: GardenManager
└── Methods:
    ├── generateSuggestions(wishlist, year)
    └── scorePlantingOption(bedId, vegetableId, year)
```

### App Controller (Global Object)

```javascript
app
├── garden: GardenManager
├── suggestionEngine: SuggestionEngine
├── currentYear: number
├── wishlist: string[]
├── currentLanguage: string
└── Methods:
    ├── init()
    ├── setLanguage(lang, save)
    ├── t(key, replacements)
    ├── changeYear(delta)
    ├── addToWishlist()
    ├── removeFromWishlist(vegetableId)
    ├── addBed()
    ├── removeBed(bedId)
    ├── openBedModal(bedId)
    ├── addPlantToBed(bedId)
    ├── removePlantFromBed(bedId, vegetableId)
    ├── saveBed(bedId)
    ├── generateSuggestions()
    ├── applySuggestion(bedId, vegetableId)
    ├── showMatrix()
    ├── closeMatrixModal()
    ├── exportData()
    ├── importData()
    ├── installAsApp()
    ├── showInstallationInstructions()
    ├── save()
    └── render()
```

---

## User Interface

### Layout Structure

**Desktop (> 968px):**
```
┌─────────────────────────────────────────────────┐
│ Header: Title + Buttons (Export/Import/Matrix)  │
│ Language: EN | DE | IT                          │
├───────────────┬─────────────────────────────────┤
│ Controls      │ Garden Beds                     │
│ (1/3 width)   │ (2/3 width)                    │
│               │                                 │
│ - Year        │ ┌────┐ ┌────┐ ┌────┐          │
│ - Wishlist    │ │Bed │ │Bed │ │Bed │          │
│ - Suggestions │ │ 1  │ │ 2  │ │ 3  │          │
│ - Bed +       │ └────┘ └────┘ └────┘          │
└───────────────┴─────────────────────────────────┘
```

**Mobile (< 480px):**
```
┌───────────────────┐
│ Header            │
│ Title             │
│ EN | DE | IT      │
│ [Button]          │
│ [Button]          │
│ [Install]         │
├───────────────────┤
│ Controls          │
│ - Year            │
│ - Wishlist        │
│ - Suggestions     │
│ - Bed +           │
├───────────────────┤
│ Garden Beds       │
│ ┌───────────────┐ │
│ │ Bed 1         │ │
│ └───────────────┘ │
│ ┌───────────────┐ │
│ │ Bed 2         │ │
│ └───────────────┘ │
└───────────────────┘
```

### Color Scheme (Earthy Tones)
```css
--soil-dark: #3a2f28      /* Primary text, dark accents */
--soil-medium: #5d4e3f    /* Secondary text, borders */
--leaf-green: #4a7c59     /* Primary color, headings */
--sage: #8ba888           /* Secondary color, light accents */
--cream: #f4f1ea          /* Background, surfaces */
--terracotta: #c1694f     /* Accent color, heavy feeders */
--sun-yellow: #e8b84d     /* Highlight, medium feeders */
--root-brown: #6b4423     /* Dark accents */
--water-blue: #7ba8a8     /* Info areas */
```

### Visual Tags & Tooltips (NEW v1.2)

**Companion Tags:**
- ✓ Green background: Good companions
- ✗ Red background: Bad companions  
- 🛡️ Blue-green gradient: Protects from pests
- 🪳 Yellow background: Shares pest vulnerabilities
- 🐞 Ladybug emoji: Attracts beneficial insects

**Individual Pest Icons (NEW):**
Each plant shows its specific vulnerabilities:
- 🐌 Slugs/Snails
- 🦟 Flying pests (aphids, flies, moths, thrips)
- 🐛 Larvae/Caterpillars (cabbage-white, hornworms, wireworms)
- 🪲 Beetles (potato-beetle, flea-beetle, japanese-beetle)

Example display:
```
🥕 Karotte (Niedrig)
   Apiaceae
   🦟 🐛    ← Pest icons with tooltips
```

**Interactive Tooltips:**
All tags have hover tooltips showing detailed information:

```
✓ Zwiebel → "Traditionell gute Begleitpflanze • Schützt vor: carrot-fly, aphids, slugs"
✗ Sellerie → "Unverträglich: Konkurriert um Nährstoffe oder hemmt Wachstum"
🛡️ Karotte → "Schützt vor: carrot-fly, aphids"
🪳 Brokkoli → "slugs, cabbage-white, aphids, cabbage-root-fly"
🐞 → "Lockt Nützlinge an: Marienkäfer, Florfliegen, Schlupfwespen, Bestäuber"
🐌 → "Schnecken: slugs"
🦟 → "Fliegende Schädlinge: aphids, carrot-fly"
🐛 → "Larven/Raupen: cabbage-white, wireworms"
🪲 → "Käfer: flea-beetle, potato-beetle"
```

**Symbol Legend:**
- Collapsible details element above garden beds
- All 5 symbols explained
- Info line: "Detailed information available by hovering over symbols"
- Fully translated (EN/DE/IT)

**Auto-Translated Bed Names (NEW):**
Default bed names automatically translate:
- English: "Bed 1, Bed 2, Bed 3"
- German: "Beet 1, Beet 2, Beet 3"
- Italian: "Aiuola 1, Aiuola 2, Aiuola 3"
- User-defined names remain unchanged in all languages

### Typography

**Font:** Inter (from rsms.me)
- **Source**: https://rsms.me/inter/
- **Type**: Variable Sans-Serif, optimized for UI
- **Features**: Ligatures, contextual alternatives
- **Fallback**: System fonts (-apple-system, etc.)

**Weights:**
- 400 (Normal): Body text, forms
- 700 (Bold): h2, h3, panel titles
- 800 (Extra Bold): h1, main heading

**Font Features Activated:**
```css
font-feature-settings: 'liga' 1, 'calt' 1;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
```

### Responsive Breakpoints

| Breakpoint | Target Devices | Layout | Special Features |
|------------|---------------|--------|------------------|
| > 968px | Desktop | 2-column (1:2) | Full features |
| 768-968px | Tablets | 1-column | Reduced spacing |
| 480-768px | Large Phones | 1-column | More compact UI |
| 375-480px | Standard Phones | 1-column | Mobile-optimized |
| < 375px | Small Phones (SE) | 1-column | Minimal padding |

**Landscape Mode (< 968px):**
- 2-column layout (1:1.5)
- Controls left, beds right
- More compact spacing

### Mobile Optimizations

**Touch Targets:**
- Minimum size: 44×44px (Apple Guidelines)
- Generous spacing between buttons
- Larger clickable areas

**Horizontal Scroll Prevention:**
```css
body, html {
    overflow-x: hidden;
    max-width: 100vw;
}
* {
    max-width: 100%;
}
```

**Responsive Elements:**
- Buttons: Full width on mobile
- Dropdown + Button: Stacked instead of side-by-side
- Modals: 95% width on mobile
- Tables: Horizontal scrollbar if needed

---

## Pest Categorization (NEW v1.2)

**Individual pest icons categorize 20+ pests into 4 visual groups:**

| Category | Icon | Pests Included |
|----------|------|----------------|
| **Slugs/Snails** | 🐌 | slugs |
| **Flying Pests** | 🦟 | aphids, whitefly, thrips, onion-fly, carrot-fly, cabbage-root-fly, leek-moth |
| **Larvae/Caterpillars** | 🐛 | cabbage-white, hornworms, pea-moth, corn-borer, earworm, wireworms, root-maggot |
| **Beetles** | 🪲 | potato-beetle, bean-beetle, cucumber-beetle, japanese-beetle, flea-beetle, squash-bug |

**Uncategorized pests** (shown in tooltips but no icon):
- spider-mites, leaf-miners

**Implementation:**
- `getPestIcons()` returns boolean flags for each category
- `getPestsByCategory()` returns actual pest lists for tooltips
- Each plant shows 0-4 icons based on its vulnerabilities
- Tooltips show category name + specific pests

**Examples:**
```
Lettuce (slugs, aphids, leaf-miners):
  → Shows: 🐌 🦟
  
Tomato (aphids, whitefly, hornworms):
  → Shows: 🦟 🐛
  
Potato (aphids, potato-beetle, wireworms):
  → Shows: 🦟 🪲 🐛
  
Onion (onion-fly, thrips):
  → Shows: 🦟
```

---

## Data Structures

### JSON Export Format

```json
{
  "vegetables": [
    {
      "id": "tomato",
      "nameEN": "Tomato",
      "nameDE": "Tomate",
      "nameIT": "Pomodoro",
      "nutrition": "high",
      "family": "Solanaceae",
      "goodCompanions": ["basil", "carrot", "lettuce"],
      "badCompanions": ["potato", "cabbage"]
    }
  ],
  "beds": [
    {
      "id": 1704636800000,
      "name": "Bed 1"
    }
  ],
  "plantings": [
    {
      "bedId": 1704636800000,
      "year": 2024,
      "vegetableId": "tomato"
    }
  ]
}
```

### LocalStorage State Format

```json
{
  "currentYear": 2024,
  "wishlist": ["tomato", "carrot", "lettuce"],
  "language": "en"
}
```

---

## PWA Manifest (inline as base64)

```json
{
  "name": "Beet Anything",
  "short_name": "Beet Anything",
  "description": "Smart garden planning with crop rotation and companion planting",
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

**Icons:** SVG with 🌱 emoji on green background

---

## Development Stages

### ✅ Stage 1: Foundation (Implemented)
- ✅ Class architecture with inheritance
- ✅ Vegetable database with companion planting information
- ✅ Data persistence (LocalStorage + Export/Import)

### ✅ Stage 2: Web Interface (Implemented)
- ✅ Complete trilingual user interface (EN/DE/IT)
- ✅ Compatibility matrix view
- ✅ Bed management with modals
- ✅ Responsive design (Desktop + Mobile)

### ✅ Stage 3: Extended Features (Implemented)
- ✅ Intelligent suggestion algorithm
- ✅ Multi-year crop rotation
- ✅ Scoring system with multiple criteria
- ✅ Automatic saving/loading
- ✅ PWA installation
- ✅ Offline functionality
- ✅ Mobile optimization (iPhone 16, Android)
- ✅ Internationalization (EN/DE/IT)

### 🔄 Stage 4: Future Features (Planned)

#### Graphical Garden Visualization
- SVG/Canvas-based representation
- Different bed shapes (rectangular, round, L-shaped)
- Geometric tools for bed layout
- Scale-accurate display with size specifications

#### Drag & Drop
- Visual moving of plants between beds
- Automatic suggestions during dragging
- Visual feedback indicators (green/red for compatibility)
- Touch-optimized for mobile

#### Individual Rule Sets
- User-defined companion planting rules
- Customizable scoring weights in algorithm
- Import/export of rule configurations
- Community-shared rule sets

#### Extended Planning
- Sowing and harvest calendar with time windows
- Plant spacing and area calculations
- Seed and material management
- Harvest quantity tracking and statistics
- Weather integration (frost warnings, etc.)

#### Extended Vegetable Database
- 50+ vegetable varieties
- Herbs and flowers
- Variety variants (e.g., different tomato types)
- Growing instructions per vegetable
- Images/photos

---

## Technical Requirements

### Browser Compatibility

**Fully Supported:**
- Chrome/Edge 90+ (Desktop & Mobile)
- Safari 14+ (Desktop & Mobile)
- Firefox 88+ (Desktop & Mobile)
- Opera 76+
- Samsung Internet 14+

**PWA Installation:**
- Chrome/Edge (Desktop & Android): Full support
- Safari iOS 11.3+: Full support
- Firefox: No PWA installation (web use only)

**Minimum Requirements:**
- ES6+ JavaScript support
- LocalStorage API
- CSS Grid & Flexbox
- Service Worker (for PWA)

### Performance

**Load Times:**
- WiFi: < 1 second
- 4G: < 2 seconds
- 3G: < 5 seconds
- Cached (after installation): < 0.5 seconds

**File Size:**
- HTML (uncompressed): ~100 KB
- With Service Worker: ~105 KB
- After minification: ~50 KB estimated
- Gzip-compressed: ~25 KB estimated

**LocalStorage:**
- Typical usage: 5-50 KB
- With 10 beds, 3 years: ~20 KB
- With 50 beds, 10 years: ~100 KB
- Limit: 5-10 MB (browser-dependent)

### Dependencies

**External Resources:**
- ✅ Inter Font (https://rsms.me/inter/inter.css)

**No Other Dependencies:**
- ❌ No framework (React, Vue, Angular)
- ❌ No UI library (Bootstrap, Tailwind)
- ❌ No build tools needed
- ❌ No backend/server required

**Advantages:**
- Simple deployment (just HTML file)
- No build pipeline needed
- Works everywhere (even offline)
- Full control over code

---

## Privacy & Security

### Data Storage
- **100% local**: All data stays in browser/device
- **No server**: No data transmission to internet
- **No tracking**: No analytics, cookies, or tracking
- **No accounts**: No login, no registration

### Sensitive Data
- **No personal data**: Only garden planning data
- **No payment data**: Free to use
- **No location data**: No GPS usage

### Data Loss Scenarios

**Data Persists:**
- ✅ Close browser/tab
- ✅ Restart computer
- ✅ Browser updates
- ✅ PWA app updates

**Data is Lost:**
- ❌ Clear browser cache completely (with "cookies and website data")
- ❌ Manually delete LocalStorage
- ❌ Uninstall browser
- ❌ Incognito/private browsing mode
- ❌ Uninstall PWA app (device-specific)

**Protection Measures:**
- Regular exports recommended (monthly)
- Backup to cloud (Dropbox, Google Drive)
- Export before major system changes

---

## Extensibility

### Add New Vegetable

**File:** `beet-anything-i18n.html`  
**Location:** `GardenManager.initializeVegetableDatabase()` (approx. line 1320)

```javascript
// Step 1: Add vegetable to list
const veggies = [
    // ... existing vegetables ...
    new Vegetable('beetroot', 'Beetroot', 'Rote Beete', 'Barbabietola', 'medium', 'Amaranthaceae'),
];

// Step 2: Set companions
this.setCompanions('beetroot',
    ['onion', 'cabbage', 'lettuce'],  // Good companions
    ['spinach', 'leek']                // Bad companions
);
```

### Add New Language

**File:** `beet-anything-i18n.html`  
**Location:** `translations` object (approx. line 1013)

```javascript
const translations = {
    en: { ... },
    de: { ... },
    it: { ... },
    fr: {  // New: French
        title: "Beet Anything",
        subtitle: "Rotation des cultures et compagnonnage faciles",
        "btn.export": "💾 Exporter les données",
        // ... all ~60 translation keys
    }
};

// Update Vegetable constructor:
class Vegetable {
    constructor(id, nameEN, nameDE, nameIT, nameFR, nutrition, family) {
        this.nameFR = nameFR;  // Add French name
        // ...
    }
    
    getName(lang = 'en') {
        if (lang === 'fr') return this.nameFR;  // Add French getter
        // ...
    }
}

// Update HTML language switch:
<button onclick="app.setLanguage('fr')" id="langFR">FR</button>
```

### Adjust Scoring Algorithm

**File:** `beet-anything-i18n.html`  
**Location:** `SuggestionEngine.scorePlantingOption()` (approx. line 1500)

```javascript
// Change weights:
score += 50;  // Family rotation (instead of 30)
score += 30;  // Nutrition rotation (instead of 25)
score += 20;  // Good companion (instead of 15)
score -= 40;  // Bad companion (instead of 30)
```

### Add New Scoring Criteria

```javascript
// Example: Consider sun requirements
if (veg.sunRequirement === 'full' && bed.location === 'south') {
    score += 20;
    reasons.push('reason.optimalSun');
}
```

### UI Customizations

**Change Color Scheme:**
```css
:root {
    --leaf-green: #2d5f3f;  /* Darker green */
    --cream: #ffffff;        /* White background */
}
```

**Adjust Font Sizes:**
```css
body {
    font-size: 1.1rem;  /* Larger (instead of 1rem) */
}
```

---

## Best Practices for Usage

### Recommended Workflow

1. **Year Start**: Set year to current year
2. **Wishlist**: Select desired vegetables for the season
3. **Generate Suggestions**: Let algorithm create recommendations
4. **Review Suggestions**: Read reasons, adjust if necessary
5. **Apply**: Accept suggestions with one click
6. **Fine-tuning**: Manual adjustments via bed modals
7. **Season End**: Advance year, history is preserved
8. **Backup**: Export data monthly

### Tips for Best Results

**Crop Rotation:**
- Build at least 3 years of history
- Same plant family minimum 3-year break
- Alternate heavy feeders and light feeders

**Companion Planting:**
- Consult matrix when unsure
- Combine multiple good companions per bed
- Definitely avoid bad companions

**Planning:**
- Keep wishlist realistic (less = better)
- More beds = more flexible planning
- Use suggestions as starting point, not dogma

**Data Security:**
- Export after every major planning change
- Backup before browser maintenance
- Cloud storage for long-term backup

---

## Known Limitations

### Functional
1. **No Season Differentiation**: Only annual planning, no early/late/succession crops
2. **No Area Calculation**: Bed size not considered
3. **No Multiple Plantings**: A bed cannot be used multiple times per year
4. **Static Companion Rules**: Hard-coded, not customizable (except in code)
5. **No Soil Value Tracking**: pH value, soil type not recorded

### Technical
1. **LocalStorage Limit**: ~5-10 MB (browser-dependent)
2. **No Cloud Sync**: Data stays on one device
3. **No Collaboration**: No multi-user operation
4. **Browser-specific**: PWA installation only in supported browsers

### Design
1. **Fixed Vegetable List**: Only 20 predefined varieties
2. **No Images**: Only text and icons
3. **No Map View**: No geographic bed representation

---

## Versioning

### Version 1.2 Pest Protection (Current)
- ✅ Complete core functionality
- ✅ **30 vegetable varieties** (up from 20)
- ✅ Trilingual (EN/DE/IT)
- ✅ **Pest protection system** (NEW!)
- ✅ **Natural pest control** through companion planting
- ✅ **Pest profiles** for all vegetables
- ✅ **Protection relationships** in UI
- ✅ **Vulnerability warnings**
- ✅ **Beneficial insect indicators**
- ✅ Auto-save/auto-load
- ✅ Export/import (with pest data)
- ✅ Enhanced suggestion algorithm
- ✅ PWA installation
- ✅ Offline functionality
- ✅ Mobile optimization (iPhone/Android)
- ✅ Inter font (rsms.me)
- ✅ Language persistence
- ✅ GitHub link in footer

### Version 1.1 i18n (February 2025)
- ✅ Italian translation added
- ✅ Language persistence
- ✅ 20 vegetables trilingual
- ✅ ~60 UI strings per language

### Planned Versions

**Version 1.3** (Q2 2025)
- Planting calendar (sowing/harvest times)
- Print function for garden plan
- Notes field per bed
- Spanish translation (ES)
- French translation (FR)

**Version 2.0** (Q4 2025)
- Graphical bed visualization
- Drag & drop interface
- User-defined rules
- Bed sizes and area calculations

**Version 2.5** (2026)
- Community features
- Rule sharing
- Multi-language (FR, ES, PT)
- Extended statistics

**Version 3.0** (2027)
- Native mobile app (Flutter/React Native)
- Cloud synchronization (optional)
- Photo upload for beds
- AI-powered problem detection

---

## Support & Documentation

### Available Documentation

1. **BEET_ANYTHING_SPECIFICATION.md** (this document)
   - Complete product description
   - Technical details
   - Extensibility

2. **BEET_ANYTHING_RESUME.md**
   - Quick reference for developers
   - Code locations
   - Common customizations

3. **APP_INSTALLATION_GUIDE.md**
   - PWA installation on all platforms
   - Step-by-step instructions
   - Troubleshooting

4. **MOBILE_OPTIMIZATION.md**
   - Responsive design details
   - Mobile-specific features
   - Testing guide

5. **README.md**
   - Project overview
   - Quick start
   - Feature list

### In-App Help

- Info boxes in panels
- Tooltips on hover (desktop)
- Explanations in modals
- Suggestions with reasons

### Code Documentation

- JSDoc comments for all classes
- Inline comments for complex logic
- English method names for business logic
- Structured code sections with dividers

---

## License & Usage

**Usage Rights:**
- ✅ Free for private use
- ✅ Modification allowed
- ✅ Distribution with attribution
- ⚠️ Commercial use only by agreement

**Open Source:**
- Code is visible (single HTML file)
- No encryption or obfuscation
- Community contributions welcome

**Liability:**
- No guarantee for correctness of growing recommendations
- Use at your own risk
- No liability for harvest losses

---

## Quick Reference: File Structure

```
beet-anything/
├── beet-anything-i18n.html              (Main app, ~105 KB)
├── BEET_ANYTHING_SPECIFICATION.md       (this document)
├── BEET_ANYTHING_RESUME.md              (Developer quick start)
├── APP_INSTALLATION_GUIDE.md            (PWA installation)
├── MOBILE_OPTIMIZATION.md               (Mobile features)
└── README.md                            (Project overview)
```

---

## Technical Stack - Summary

| Component | Technology | Version |
|-----------|------------|---------|
| Frontend | Pure HTML/CSS/JS | ES6+ |
| Styling | Custom CSS | CSS3 |
| Layout | CSS Grid + Flexbox | - |
| Font | Inter (rsms.me) | Variable Font |
| i18n | Custom system | EN/DE/IT |
| Persistence | LocalStorage API | - |
| PWA | Service Worker | - |
| Offline | Cache API | - |
| Icons | SVG + Emoji | - |
| Build | No tools needed | - |
| Hosting | Static web server | - |

**No external JavaScript libraries!**

---

**Created**: 2025  
**Product Name**: Beet Anything  
**Version**: 1.2 Pest Protection  
**Status**: Production Ready  
**Filename**: beet-anything-i18n.html  
**Last Updated**: February 2025  
**GitHub**: https://github.com/schatzl/beet-anything
