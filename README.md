# 🌱 Beet Anything

**Intelligent Garden Planning with Crop Rotation, Companion Planting & Pest Protection**

A modern, self-contained Progressive Web App for planning your vegetable garden across multiple years, considering crop rotation rules, companion planting relationships, and natural pest protection strategies.

*A 24h vibe coding project*

**Version**: 1.2 Pest Protection  
**Last Updated**: February 2025  
**Status**: Production Ready  
**Languages**: English, German, Italian  
**File**: beet-anything.html  
**GitHub**: https://github.com/schatzl/beet-anything  
**License**: Free for any use - Personal, commercial, educational, or otherwise.  
**Live demo**: [Beet Anything](https://target23.de/beet-anything.html)

---

## ✨ Features

### 🗓️ Multi-Year Planning
- Plan unlimited years into the future and past
- Track complete planting history for each bed
- View previous year's crops for better rotation planning
- Navigate easily between years with arrow buttons

### 🏡 Flexible Garden Management
- Create unlimited garden beds
- Name each bed individually
- Assign multiple vegetables per bed and year
- Visual overview of all beds and their plantings

### 🌿 Smart Crop Rotation
- Intelligent algorithm considers plant families
- Recommends optimal rotation to prevent soil fatigue
- Balances nutrition demands (heavy/medium/light feeders)
- Warns about same family planting in consecutive years

### 🤝 Companion Planting
- Built-in database of 30 vegetables with proven relationships
- Shows good companions (mutually beneficial)
- Warns about bad companions (incompatible)
- Visual compatibility matrix for all combinations

### 🛡️ Pest Protection System (NEW!)
- **Natural pest control** through companion planting
- **30 vegetables** with complete pest profiles
- **Protection relationships**: Shows which plants protect others from pests
- **Vulnerability warnings**: Alerts when plants share pest susceptibilities
- **Beneficial insects**: Identifies plants that attract helpful bugs
- **Smart scoring**: Algorithm prioritizes pest-protective combinations
- **Interactive tooltips**: Hover over any tag to see detailed information
  - Why plants are good/bad companions
  - Which specific pests are shared or repelled
  - Which beneficial insects are attracted
- **Individual pest indicators**: Each plant shows its vulnerabilities
  - 🐌 Slugs/Snails
  - 🦟 Flying pests (aphids, flies, moths)
  - 🐛 Larvae/Caterpillars (cabbage-white, hornworms)
  - 🪲 Beetles (flea-beetle, potato-beetle)
- **Comprehensive legend**: All symbols explained with hover instructions
- **20+ common pests** tracked: slugs, aphids, cabbage-white, carrot-fly, etc.
- **Critical slug protection**: 14 vulnerable plants, 5 protective plants

### 🌍 Full Internationalization
- **3 languages**: English, German, Italian
- **Complete UI translation**: All buttons, labels, messages
- **Vegetable names**: Trilingual (30 vegetables × 3 languages)
- **Auto-translated bed names**: Default names adapt to language
  - EN: "Bed 1, Bed 2, Bed 3"
  - DE: "Beet 1, Beet 2, Beet 3"
  - IT: "Aiuola 1, Aiuola 2, Aiuola 3"
- **Language persistence**: Remembers your choice
- **Instant switching**: Change language anytime

### 🎯 Suggestion System
- One-click garden plan generation
- Considers:
  - Crop rotation rules
  - Companion planting compatibility
  - Nutrition rotation
  - Previous plantings (2-year history)
  - **Pest protection synergies** (NEW!)
  - **Shared pest vulnerabilities** (NEW!)
  - **Beneficial insect attraction** (NEW!)
- Detailed explanations for each suggestion
- Apply suggestions individually or all at once

### 💾 Data Management
- **Auto-save**: Every change saved automatically to LocalStorage
- **Auto-load**: All data restored on app startup
- **Export**: Download complete garden data as JSON
- **Import**: Restore data from backup files
- **Version migration**: Automatically upgrades old data formats (v1.0 → v1.2)
- **Clear all data**: Fresh start option with confirmation
- **Privacy**: 100% local storage, no server uploads

**Data Versioning:**
- Current version: **1.2**
- Automatic migration from v1.0 (legacy) to v1.2
- Old saves get pest data added automatically
- Console logging shows migration progress

### 📱 Progressive Web App
- **Install as app** on iPhone, Android, or Desktop
- **Works offline** after first visit
- **Fullscreen mode** when installed
- **Fast loading** from cache
- **Automatic updates** when online

### 🌍 Multilingual
- **English** (Default)
- **German** (Deutsch)
- **Italian** (Italiano)
- **Language persistence**: Remembers your choice
- **All content translated**: UI, vegetables, reasons

### 📱 Mobile Optimized
- Fully responsive design
- Touch-friendly interface (44×44px targets)
- Optimized for iPhone SE to iPhone 16 Pro Max
- Works on all Android devices
- Landscape mode support
- No horizontal scroll on any device

---

## 🚀 Quick Start

### Option 1: Use Online

1. Visit hosted version (if available)
2. Start planning immediately
3. No installation required

### Option 2: Install as App

**iPhone/iPad (Safari):**
```
1. Open in Safari
2. Tap Share (□↑)
3. Select "Add to Home Screen"
4. Tap "Add"
```

**Android (Chrome):**
```
1. Open in Chrome
2. Tap "Install app" prompt
   OR Menu (⋮) → "Install app"
3. Confirm installation
```

**Desktop (Chrome/Edge):**
```
1. Click ⊕ icon in address bar
   OR Menu (⋮) → "Install"
2. Click "Install"
```

See [APP_INSTALLATION_GUIDE.md](APP_INSTALLATION_GUIDE.md) for detailed instructions.

### Option 3: Run Locally

```bash
# Download the file
wget beet-anything.html

# Open in browser
# Double-click the file
# OR serve with Python:
python3 -m http.server 8000
# Visit http://localhost:8000/beet-anything.html
```

---

## 📖 How to Use

### 1. Set Up Your Garden

1. **Add Beds**
   - Click "+ Add Garden Bed"
   - Name your beds (e.g., "North Bed", "Bed 1", "Tomato Patch")

2. **Select Year**
   - Use ← → buttons to navigate years
   - Current year is displayed prominently

### 2. Plan Your Crops

**Method A: Manual Planning**
1. Click on any bed
2. Select vegetables from dropdown
3. Click "Add Plant"
4. Repeat for all beds

**Method B: Use Suggestions (Recommended)**
1. Add vegetables to your Wishlist
2. Click "✨ Suggest Garden Plan"
3. Review suggestions with reasons
4. Click "Apply to Bed" for each suggestion

### 3. Review & Adjust

- View compatibility indicators (✓ good, ✗ bad companions)
- Check nutrition badges (high/medium/low)
- See previous year plantings below each bed
- Make manual adjustments as needed

### 4. Track Over Years

- Advance to next year (→ button)
- Previous plantings are preserved
- History helps with rotation planning
- Algorithm considers multi-year history

### 5. Backup Your Data

- Click "💾 Export Data" regularly
- Save JSON file to cloud storage
- Import on new devices or after reset

---

## 🌿 Included Vegetables

### 30 Varieties with Full Data

**Original 20:**
- Tomato, Potato, Carrot, Lettuce, Cabbage
- Beans, Peas, Onion, Garlic
- Cucumber, Zucchini, Corn, Radish
- Spinach, Basil, Pepper, Celery
- Arugula, Kohlrabi, Leek

**New 10 (v1.2):**
- Broccoli, Chives, Parsley, Pumpkin, Mint
- Strawberry, Turnip, Rhubarb, Eggplant, Fennel

### Data per Vegetable:
- ✅ Names in 3 languages (EN/DE/IT)
- ✅ Nutrition demand (high/medium/low)
- ✅ Plant family
- ✅ Good companion plants
- ✅ Bad companion plants
- ✅ **Pest susceptibilities** (NEW!)
- ✅ **Pests it protects against** (NEW!)
- ✅ **Attracts beneficial insects** (NEW!)

### Example Pest Profiles:

| Vegetable | Susceptible To | Protects Against | Beneficials |
|-----------|----------------|------------------|-------------|
| **Onion** | Onion-fly, Thrips | Carrot-fly, Aphids, Slugs | ❌ |
| **Garlic** | Onion-fly | Aphids, Slugs, Japanese-beetle | ❌ |
| **Chives** | - | Aphids, Carrot-fly, Slugs, Japanese-beetle | ✅ |
| **Basil** | Aphids, Japanese-beetle, Slugs | Aphids, Whitefly, Hornworms | ✅ |
| **Mint** | Aphids, Spider-mites | Aphids, Cabbage-white, Flea-beetle, Slugs | ✅ |
| **Fennel** | Aphids | Aphids, Slugs | ✅ |
| **Lettuce** | Slugs, Aphids, Leaf-miners | - | ❌ |
| **Cabbage** | Cabbage-white, Aphids, Cabbage-root-fly, Slugs | - | ❌ |
| **Strawberry** | Slugs, Aphids, Spider-mites | - | ❌ |
| **Carrot** | Carrot-fly, Aphids, Wireworms | - | ❌ |

**Key Insights:**
- 🐌 **Slugs**: 14 plants vulnerable, 5 plants protective (Onion family + Mint + Fennel)
- 🪲 **Aphids**: Most common pest, many protective plants available
- 🐞 **Beneficial attractors**: Chives, Basil, Mint, Fennel, Beans, Peas, Parsley

---

## 🧮 How the Algorithm Works

### Scoring System

The suggestion algorithm evaluates each vegetable-bed combination and assigns a score based on multiple criteria:

#### Family Rotation (+30/-20 points)
- **+30**: Different plant family than previous year ✅
- **-20**: Same plant family as previous year ⚠️

*Why*: Prevents soil-borne diseases and pest accumulation

#### Nutrition Rotation (+25/-15 points)
- **+25**: Light feeder after heavy feeder (soil regeneration) ✅
- **-15**: Heavy feeder after heavy feeder (soil depletion) ⚠️
- **+10**: Light feeder generally (soil-friendly) ✅

*Why*: Balances soil nutrients over time

#### Companion Planting (+15/-30 points)
- **+15**: Per good companion already in bed ✅
- **-30**: Per bad companion already in bed ⚠️

*Why*: Maximizes beneficial plant interactions

#### Pest Protection (+20/-15 points) *NEW!*
- **+20**: Protects other plants from pests ✅ 🛡️
- **-15**: Shares pest vulnerabilities with others ⚠️ 🦟
- **+10**: Attracts beneficial insects ✅ 🐞

*Why*: Natural pest control through companion planting

#### Other Factors
- **+5**: Empty bed (more flexibility)
- **-10**: Same plant grown 2 years ago (extended rotation)

### Result

Vegetables are assigned to beds with highest scores, ensuring:
- Optimal crop rotation
- Compatible plant combinations
- **Natural pest protection** (NEW!)
- Soil health preservation
- Maximum harvest potential

---

## 💡 Tips for Best Results

### Crop Rotation Best Practices

1. **Build History**
   - Track at least 3 years of plantings
   - More history = better suggestions

2. **Respect Plant Families**
   - Never plant same family in consecutive years
   - Minimum 3-year gap for same family

3. **Balance Nutrition**
   - Follow heavy feeders with light feeders
   - Give soil time to regenerate

### Companion Planting Tips

1. **Check the Matrix**
   - Click "📊 View Matrix" for all combinations
   - Green ✓ = good companions
   - Red ✗ = avoid together

2. **Maximize Benefits**
   - Combine multiple good companions when possible
   - Examples:
     - Tomatoes + Basil + Carrot
     - Beans + Corn + Cucumber ("Three Sisters")

3. **Avoid Conflicts**
   - Never ignore bad companion warnings
   - Even if space is limited, find alternative arrangements

### Pest Protection Strategies (NEW!)

1. **Use Protective Plants**
   - Plant onions near carrots → protects from carrot-fly
   - Plant garlic near strawberries → repels aphids and slugs
   - Plant chives near roses → deters aphids

2. **Attract Beneficial Insects**
   - Look for 🐞 emoji in plant metadata
   - Plants like basil, mint, fennel attract:
     - Ladybugs (eat aphids)
     - Lacewings (eat aphids and thrips)
     - Parasitic wasps (control caterpillars)

3. **Avoid Clustering Vulnerabilities**
   - Don't plant cabbage + broccoli + kohlrabi together
   - All attract same pests (cabbage-white butterfly)
   - Algorithm warns with ⚠️ 🦟 tags

4. **Watch for Protection Tags**
   - 🛡️ Green tag = This plant protects others
   - ⚠️ 🦟 Yellow tag = Plants share pest problems
   - 🐞 Emoji = Attracts beneficial insects

### Example Combinations

**✅ EXCELLENT: Carrot + Onion + Chives**
- Onion protects carrot from carrot-fly and slugs
- Chives attracts beneficials
- All have different nutrition needs
- Different families
- **Tooltip on 🛡️ Onion**: "Protects from: carrot-fly, aphids, slugs"

**✅ GREAT: Tomato + Basil**
- Basil protects tomato from aphids and whitefly
- Basil attracts pollinators
- Traditional good companions
- Algorithm gives +45 bonus points!
- **Tooltip on ✓ Basil**: "Traditional good companion • Protects from: aphids, whitefly, hornworms"

**✅ PERFECT: Lettuce + Chives**
- Chives protects lettuce from slugs and aphids
- Both vulnerable to slugs → Chives provides critical protection
- **Tooltip on 🛡️ Chives**: "Protects from: aphids, carrot-fly, slugs, japanese-beetle"

**❌ AVOID: Cabbage + Broccoli + Kohlrabi**
- All Brassicaceae family
- Share pests (cabbage-white, aphids, slugs)
- Heavy feeders compete for nutrients
- Algorithm warns heavily (-50 points)
- **Tooltip on 🪳 Broccoli**: "slugs, cabbage-white, aphids, cabbage-root-fly"

### Visual Indicators

**Pest Icons (Individual Plants):**
Each plant displays icons for its pest vulnerabilities:

```
🥕 Karotte
  Apiaceae
  🦟 🐛    ← Shows: Flying pests + Larvae
  
🥬 Salat
  Asteraceae
  🐌 🦟 🐛  ← Shows: Slugs + Flying pests + Larvae
  
🧅 Zwiebel
  Amaryllidaceae
  🦟       ← Shows: Only flying pests
```

**Hover for details:**
- 🐌 → "Slugs/Snails: slugs"
- 🦟 → "Flying pests (aphids, flies, moths): aphids, carrot-fly"
- 🐛 → "Larvae/Caterpillars: cabbage-white, wireworms"
- 🪲 → "Beetles: flea-beetle, potato-beetle"

**Benefits:**
- See vulnerabilities at a glance
- Works for single plants (not just in combinations)
- Categorized by pest type
- Detailed tooltips with specific pest names

### Data Management

1. **Export Regularly**
   - Monthly exports recommended
   - Before any system changes
   - Keep in cloud storage

2. **Backup Before**
   - Clearing browser cache
   - Updating device OS
   - Switching devices
   - Uninstalling app

3. **Version Migration**
   - App automatically upgrades old data formats
   - v1.0 (legacy) → v1.2 adds pest protection data
   - Console shows migration progress
   - No manual intervention needed

4. **Fresh Start**
   - Use "🗑️ Clear All Data" button for complete reset
   - Confirmation required before deletion
   - All data removed, page reloads fresh

5. **Use Meaningful Bed Names**
   - "North Bed" better than "Bed 1"
   - "Tomato Patch" helps remember layout
   - "Raised Bed A" for structured gardens

---

## 🔧 Technical Details

### Technology Stack

- **Frontend**: Pure HTML/CSS/JavaScript (ES6+)
- **Styling**: Custom CSS with CSS Grid & Flexbox
- **Font**: Inter Variable Font (rsms.me)
- **Storage**: LocalStorage API
- **PWA**: Service Worker + Web App Manifest
- **Dependencies**: Zero (except Inter font CDN)

### Browser Support

| Browser | Version | PWA Install | Offline |
|---------|---------|-------------|---------|
| Chrome | 90+ | ✅ Yes | ✅ Yes |
| Edge | 90+ | ✅ Yes | ✅ Yes |
| Safari | 14+ | ✅ Yes | ✅ Yes |
| Firefox | 88+ | ❌ No | ✅ Yes |
| Samsung Internet | 14+ | ✅ Yes | ✅ Yes |

### File Structure

```
beet-anything.html          (~115 KB)
├── HTML Structure
├── CSS Styling (inline)
├── JavaScript Logic (inline)
├── Translations (EN/DE/IT)
├── Service Worker (inline)
└── Web App Manifest (inline, base64)
```

**Single File** - Everything is self-contained!

### Performance

- **Load Time**: < 1s on WiFi, < 2s on 4G
- **File Size**: ~115 KB uncompressed, ~30 KB gzipped
- **Memory**: ~5-50 KB in LocalStorage (typical usage)
- **Offline**: Full functionality after first visit

---

## 📚 Documentation

### For Users
- **[APP_INSTALLATION_GUIDE.md](APP_INSTALLATION_GUIDE.md)** - How to install as PWA
- **[MOBILE_OPTIMIZATION.md](MOBILE_OPTIMIZATION.md)** - Mobile features & testing
- **This README** - Getting started & usage

### For Developers
- **[BEET_ANYTHING_SPECIFICATION.md](BEET_ANYTHING_SPECIFICATION.md)** - Complete technical spec
- **[BEET_ANYTHING_RESUME.md](BEET_ANYTHING_RESUME.md)** - Developer quick reference

---

## 🛠️ Customization

### Add New Vegetable

**Location**: Line ~1320 in HTML file

```javascript
// Add to vegetable list
new Vegetable('beetroot', 'Beetroot', 'Rote Beete', 'Barbabietola', 'medium', 'Amaranthaceae'),

// Set companions
this.setCompanions('beetroot',
    ['onion', 'cabbage'],     // Good companions
    ['spinach', 'leek']       // Bad companions
);
```

### Add New Language

**Location**: Line ~1013 in HTML file

```javascript
// Add translation object
fr: {
    title: "Beet Anything",
    subtitle: "Rotation des cultures facile",
    // ... ~60 translation keys
}

// Update Vegetable class
constructor(id, nameEN, nameDE, nameIT, nameFR, ...) {
    this.nameFR = nameFR;
}

// Add button to HTML
<button onclick="app.setLanguage('fr')">FR</button>
```

### Adjust Algorithm

**Location**: Line ~1500 in HTML file

```javascript
// Change scoring weights
score += 50;  // Family rotation (was 30)
score -= 50;  // Bad companion (was 30)
```

See [BEET_ANYTHING_RESUME.md](BEET_ANYTHING_RESUME.md) for more customization options.

---

## 🚢 Deployment

### Static Hosting (Recommended)

**GitHub Pages** (Free):
```bash
1. Create GitHub repo
2. Upload beet-anything.html as index.html
3. Enable GitHub Pages
4. Visit https://username.github.io/repo-name
```

**Netlify** (Free):
```bash
1. Drag & drop HTML file to Netlify
2. Rename to index.html
3. Get URL: https://your-site.netlify.app
```

**Vercel** (Free):
```bash
1. Import GitHub repo to Vercel
2. Auto-deploy on push
3. Get URL: https://your-site.vercel.app
```

### Requirements

- **HTTPS**: Required for PWA installation
- **Static Server**: No backend needed
- **Single File**: Just upload the HTML file
- **No Build**: No compilation or bundling needed

---

## 🔒 Privacy & Security

### Data Privacy

✅ **100% Local** - All data stays on your device  
✅ **No Server** - No uploads to any server  
✅ **No Tracking** - No analytics or cookies  
✅ **No Accounts** - No login required  
✅ **No Personal Data** - Only garden planning info  

### Data Security

- LocalStorage is browser-specific
- Data encrypted at rest (browser handles)
- HTTPS in transit (when hosted)
- Export for backup recommended

### Data Loss Risks

❌ **You will lose data if:**
- Clear browser cache (with "cookies and site data")
- Uninstall PWA app
- Use incognito/private mode
- Switch devices without export

✅ **Protect your data:**
- Export regularly (monthly)
- Keep backups in cloud
- Import after reinstalling

---

## 🗺️ Roadmap

### Version 1.2 (Q2 2025)
- [ ] 30+ vegetables
- [ ] Planting calendar (sowing/harvest dates)
- [ ] Print function
- [ ] Notes per bed
- [ ] French translation

### Version 2.0 (Q4 2025)
- [ ] Graphical garden visualization
- [ ] Drag & drop plants between beds
- [ ] User-defined companion rules
- [ ] Bed size management

### Version 2.5 (2026)
- [ ] Cloud sync (optional)
- [ ] Community rule sharing
- [ ] Spanish & Portuguese
- [ ] Photo uploads

### Version 3.0 (2027)
- [ ] Native mobile app
- [ ] AI-powered suggestions
- [ ] Weather integration
- [ ] Harvest tracking

---

## 🤝 Contributing

This is currently a personal project, but contributions are welcome!

### How to Contribute

1. **Report Bugs**
   - Describe the issue
   - Include browser/device info
   - Steps to reproduce

2. **Suggest Features**
   - Explain use case
   - Why it's useful
   - How it should work

3. **Submit Code**
   - Fork the project
   - Make changes
   - Test thoroughly
   - Submit pull request

4. **Improve Documentation**
   - Fix typos
   - Add examples
   - Translate to other languages

5. **Share Companion Planting Data**
   - Suggest new vegetables
   - Correct companion relationships
   - Provide sources

---

## ⚖️ License

**For Private Use**: Free to use, modify, and share

**For Commercial Use**: Contact required

**Attribution**: Appreciated but not required

**No Warranty**: Use at your own risk. No guarantee of accuracy for growing recommendations.

---

## 🙏 Acknowledgments

### Data Sources
- Companion planting relationships based on traditional gardening knowledge
- Plant families and nutrition demands from horticultural references

### Technologies
- **Inter Font** by Rasmus Andersson (https://rsms.me/inter/)
- **PWA Best Practices** from web.dev
- **Mobile Optimization** following Apple & Material Design guidelines

### Inspiration
- Traditional crop rotation practices
- Permaculture principles
- Square foot gardening methods

---

## 📞 Support

### Getting Help

- **Installation Issues**: See [APP_INSTALLATION_GUIDE.md](APP_INSTALLATION_GUIDE.md)
- **Usage Questions**: Check this README
- **Technical Details**: See [BEET_ANYTHING_SPECIFICATION.md](BEET_ANYTHING_SPECIFICATION.md)
- **Mobile Problems**: See [MOBILE_OPTIMIZATION.md](MOBILE_OPTIMIZATION.md)

### Feedback

Found a bug? Have a feature idea? Want to contribute?

- Create an issue on GitHub
- Send feedback through app (thumbs down button)
- Contact via email (if provided)

---

## 📜 Changelog

### v1.2 Pest Protection (February 2025)
- ✨ **Pest Protection System** - Natural pest control through companion planting
- ✨ Added 10 new vegetables (now 30 total)
- ✨ Pest profiles for all 30 vegetables
- ✨ Algorithm considers pest protection (+20/-15 points)
- ✨ UI shows protection relationships (🛡️ tags)
- ✨ UI warns about shared pests (🪳 tags)
- ✨ **Individual pest icons** per plant (🐌🦟🐛🪲)
- ✨ Beneficial insect indicators (🐞 emoji)
- ✨ **Interactive tooltips** for all tags
- ✨ **Symbol legend** with hover instructions
- ✨ **Auto-translated bed names** (Bed/Beet/Aiuola)
- ✨ **Data versioning system** - Automatic migration from v1.0
- ✨ **Clear All Data** button - Fresh start option
- ✨ Comprehensive slug protection (14 vulnerable, 5 protective plants)
- ✨ 15 new translation keys (tooltips + pest categories + data management)
- 📝 Complete pest data research and integration
- 🎨 New CSS styles for pest icons and tooltips
- 🔧 Migration system for backwards compatibility

### v1.1 i18n (February 2025)
- ✨ Added Italian translation
- ✨ Language persistence (remembers choice)
- ✨ All vegetables trilingual (EN/DE/IT)
- ✨ Complete UI translation (~60 strings)
- ✨ Language switch in header
- 🐛 Fixed mobile layout issues
- 📝 Updated all documentation to English

### v1.0 PWA (January 2025)
- ✨ Initial release
- ✨ 20 vegetables with companion data
- ✨ Multi-year planning
- ✨ Suggestion algorithm
- ✨ PWA installation
- ✨ Auto-save/auto-load
- ✨ Mobile optimization
- ✨ Offline functionality
- ✨ English & German languages

---

## 🌟 Star Features

### What Makes Beet Anything Special?

1. **Zero Dependencies**
   - Single HTML file
   - No build tools
   - No frameworks
   - Works anywhere

2. **Privacy First**
   - 100% local storage
   - No server required
   - No tracking
   - No accounts

3. **Progressive Enhancement**
   - Works in browser
   - Better as installed app
   - Offline capable
   - Auto-updating

4. **Smart Algorithm**
   - Multiple criteria
   - Detailed explanations
   - Balanced recommendations
   - Years of planning

5. **Truly Multilingual**
   - Not just UI translated
   - Vegetable names in 3 languages
   - Reasons and explanations
   - Seamless switching

---

**Made with 🌱 for gardeners who care about healthy soil and happy plants**

*Happy Planning! 🌿🥕🍅🐞*
