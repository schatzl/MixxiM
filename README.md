# 🌱 Beet Anything

**Intelligent Garden Planning with Crop Rotation and Companion Planting**

A one-hour vibe coding project.

A modern, self-contained Progressive Web App for planning your vegetable garden across multiple years, considering crop rotation rules and companion planting relationships.

**Version**: 1.1 i18n  
**Languages**: English, German, Italian  
**Status**: Beta  
**License**: Free for private use
**Preview**: [Staging site](https://target23.de/beet-anything.html)

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
- Built-in database of 20 vegetables with proven relationships
- Shows good companions (mutually beneficial)
- Warns about bad companions (incompatible)
- Visual compatibility matrix for all combinations

### 🎯 Suggestion System
- One-click garden plan generation
- Considers:
  - Crop rotation rules
  - Companion planting compatibility
  - Nutrition rotation
  - Previous plantings (2-year history)
- Detailed explanations for each suggestion
- Apply suggestions individually or all at once

### 💾 Data Management
- **Auto-save**: Every change saved automatically to LocalStorage
- **Auto-load**: All data restored on app startup
- **Export**: Download complete garden data as JSON
- **Import**: Restore data from backup files
- **Privacy**: 100% local storage, no server uploads

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
wget beet-anything-i18n.html

# Open in browser
# Double-click the file
# OR serve with Python:
python3 -m http.server 8000
# Visit http://localhost:8000/beet-anything-i18n.html
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

### 20 Varieties with Full Data

| Vegetable | EN | DE | IT | Nutrition | Family |
|-----------|----|----|-----|-----------|--------|
| Tomato | Tomato | Tomate | Pomodoro | High | Solanaceae |
| Potato | Potato | Kartoffel | Patata | High | Solanaceae |
| Carrot | Carrot | Karotte | Carota | Low | Apiaceae |
| Lettuce | Lettuce | Salat | Lattuga | Low | Asteraceae |
| Cabbage | Cabbage | Kohl | Cavolo | High | Brassicaceae |
| Beans | Beans | Bohnen | Fagioli | Low | Fabaceae |
| Peas | Peas | Erbsen | Piselli | Low | Fabaceae |
| Onion | Onion | Zwiebel | Cipolla | Medium | Amaryllidaceae |
| Garlic | Garlic | Knoblauch | Aglio | Medium | Amaryllidaceae |
| Cucumber | Cucumber | Gurke | Cetriolo | Medium | Cucurbitaceae |
| Zucchini | Zucchini | Zucchini | Zucchina | Medium | Cucurbitaceae |
| Corn | Corn | Mais | Mais | High | Poaceae |
| Radish | Radish | Radieschen | Ravanello | Low | Brassicaceae |
| Spinach | Spinach | Spinat | Spinaci | Medium | Amaranthaceae |
| Basil | Basil | Basilikum | Basilico | Low | Lamiaceae |
| Pepper | Pepper | Paprika | Peperone | Medium | Solanaceae |
| Celery | Celery | Sellerie | Sedano | High | Apiaceae |
| Arugula | Arugula | Rucola | Rucola | Low | Brassicaceae |
| Kohlrabi | Kohlrabi | Kohlrabi | Cavolo Rapa | Medium | Brassicaceae |
| Leek | Leek | Lauch | Porro | Medium | Amaryllidaceae |

**Each vegetable includes:**
- Names in 3 languages
- Nutrition demand level
- Plant family
- List of good companions
- List of bad companions

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

#### Other Factors
- **+5**: Empty bed (more flexibility)
- **-10**: Same plant grown 2 years ago (extended rotation)

### Result

Vegetables are assigned to beds with highest scores, ensuring:
- Optimal crop rotation
- Compatible plant combinations
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

3. **Use Meaningful Bed Names**
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
beet-anything-i18n.html          (~105 KB)
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
- **File Size**: ~105 KB uncompressed, ~25 KB gzipped
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
2. Upload beet-anything-i18n.html as index.html
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

**Version**: 1.1 i18n  
**Last Updated**: February 2025  
**Status**: Beta
**File**: beet-anything-i18n.html

---

*Happy Planning! 🌿🥕🍅*
