# CROUS Lyon Housing Scraper 🏠

Get **push notifications** when CROUS housing becomes available in Lyon - no email credentials needed!

## How It Works

```
┌──────────────────────────────────────────────────────────────┐
│                    GitHub Actions (every 5 min)               │
│                                                               │
│   Scrape CROUS ──▶ New housing? ──▶ Create GitHub Issue      │
│                         │                    │                │
│                         ▼                    ▼                │
│                        NO                   YES               │
│                    (do nothing)     (you get notified!)      │
└──────────────────────────────────────────────────────────────┘
```

**GitHub notifies you automatically** via:
- 📱 **Push notification** (GitHub mobile app)
- 📧 **Email** (your GitHub account email)
- 🔔 **Web notification** (github.com)

---

## 🚀 Setup (5 minutes)

### Step 1: Fork or Create Repo

Option A - Fork this repo, or

Option B - Create new repo:
```bash
cd /home/erdos/crous
git init
git add .
git commit -m "Initial commit"
# Create repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/crous-lyon.git
git push -u origin main
```

### Step 2: Enable Actions

Go to your repo → **Actions** tab → Enable workflows

### Step 3: Configure Notifications (optional)

Go to https://github.com/settings/notifications and ensure:
- ✅ "Participating and @mentions" notifications are ON
- ✅ "Issues" notifications are enabled for your repo

Install **GitHub Mobile** for push notifications:
- [iOS](https://apps.apple.com/app/github/id1477376905)
- [Android](https://play.google.com/store/apps/details?id=com.github.android)

---

## ✅ That's it!

When new housing is found, you'll get a notification like:

> 🏠 **2 New CROUS Housing ⭐ PRIORITY** - 18/12/2024
> 
> | Résidence | Distance | Link |
> |-----------|----------|------|
> | Benjamin Delessert ⭐ | 2.3 km | [Apply](link) |
> | Condorcet | 1.8 km | [Apply](link) |

---

## 🎛️ Customization

### Change Reference Campus

Edit `lyon-crous-scraper.js`:

```javascript
const CAMPUS_REFERENCE_COORDS = {
  lat: 45.7827,  // Your latitude
  lng: 4.8771,   // Your longitude
  name: 'Your Campus',
  address: 'Your address'
};
```

**Lyon campuses:**
| Campus | Coordinates |
|--------|-------------|
| Lyon 1 La Doua | `45.7827, 4.8771` |
| Lyon 2 Berges du Rhône | `45.7525, 4.8350` |
| Lyon 3 Manufacture | `45.7470, 4.8630` |
| INSA Lyon | `45.7820, 4.8760` |
| ENS Lyon | `45.7295, 4.8270` |

### Change Priority Residences

```javascript
const priorityResidences = [
  'Benjamin Delessert',
  'Your Preferred',
  // ...
];
```

### Change Check Frequency

Edit `.github/workflows/crous-check.yml`:

```yaml
schedule:
  - cron: '*/5 * * * *'   # Every 5 minutes (default)
  - cron: '*/10 * * * *'  # Every 10 minutes
  - cron: '0 * * * *'     # Every hour
```

---

## 📁 Project Files

```
crous/
├── lyon-crous-scraper.js    # Main script
├── package.json             # Dependencies
├── sent_offers.json         # Cache (auto-generated)
├── .gitignore
└── .github/workflows/
    └── crous-check.yml      # GitHub Actions
```

---

## ❓ FAQ

**Q: Do I need any credentials?**  
A: No! Uses GitHub's built-in `GITHUB_TOKEN` automatically.

**Q: Will I get spammed?**  
A: No, only notified for NEW housing (uses cache).

**Q: Is it free?**  
A: Yes, GitHub Actions free tier is plenty.

**Q: How do I stop notifications?**  
A: Disable the workflow in Actions tab.

**Q: Can I test it manually?**  
A: Yes! Actions → "CROUS Lyon Housing Check" → "Run workflow"
