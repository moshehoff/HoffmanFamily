# Hoffman Family History

This repository contains the family history website for the Hoffman family, built using the [Family History Platform](https://github.com/moshehoff/family_history_platform).

## 🌐 Live Site

Visit the live site at: https://moshehoff.github.io/HoffmanFamily/

## 📁 Repository Structure

```
HoffmanFamily/
├── platform/                      # Family History Platform (submodule)
├── data/
│   ├── hochman.ged                # Hochman family GEDCOM file
│   ├── zitserman.ged             # Zitserman family GEDCOM file
│   └── place_mappings.json        # Place to Wikipedia mappings
├── bios/                          # Extended biographies by person ID
│   ├── I11032861/
│   │   ├── 01-early-life.md
│   │   └── 02-career.md
│   └── I38516664/
├── documents/                     # Photos and documents by person ID
│   ├── I10847256/
│   │   ├── photo1.jpg
│   │   └── photo1.md
│   └── I11052340/
├── content/                       # Static pages
│   ├── index.md
│   └── pages/
│       ├── about.md
│       ├── preface.md
│       └── founders.md
├── public/                        # Pre-built site (generated, committed for deployment)
├── config/
│   └── family-config.json         # Site configuration
└── .github/
    └── workflows/
        └── deploy.yml             # GitHub Actions deployment (pre-built only)
```

## 🚀 Building the Site Locally

### Prerequisites

- Python 3.11+
- Node.js 22+
- Git with submodules initialized

### Build Steps

1. **Clone with submodules**:
```bash
git clone --recursive https://github.com/moshehoff/HoffmanFamily.git
cd HoffmanFamily
```

2. **Generate profiles**:
```bash
python platform/scripts/doit.py \
  --bios-dir bios \
  --src-content-dir content \
  --output platform/site/content/profiles \
  data/hochman.ged data/zitserman.ged
```

3. **Build the site**:
```bash
cd platform/site
npm install
npx quartz build
cd ../..
```

4. **Preview locally**:
```bash
cd platform/site
npx quartz serve
```

Visit http://localhost:8080

## 🚀 Deploying to GitHub Pages

The site uses a pre-built deployment workflow (like FamilyHistory). To deploy:

1. **Build the site locally** (see "Building the Site Locally" above)

2. **Copy built files to main repo**:
   ```bash
   # On Windows PowerShell:
   Copy-Item -Recurse platform/site/public public
   
   # On Linux/Mac:
   cp -r platform/site/public ./public
   ```

3. **Commit and push**:
   ```bash
   git add -f public/
   git commit -m "Deploy: update pre-built site"
   git push origin main
   ```

The GitHub Actions workflow will automatically deploy when `public/` changes.

**Note:** Make sure GitHub Pages is configured to use "GitHub Actions" as the source (Settings → Pages).

## 📝 Making Changes

### Updating Family Data

1. Edit GEDCOM files (`data/hochman.ged` and/or `data/zitserman.ged`) in your genealogy software
2. Export and replace the GEDCOM file(s)
3. Rebuild: `python platform/scripts/doit.py --bios-dir bios --src-content-dir content --output platform/site/content/profiles data/hochman.ged data/zitserman.ged`

### Adding Biographies

Create a directory for the person (using their ID from GEDCOM):

```bash
mkdir bios/I12345
echo "# Early Life\n\nContent here..." > bios/I12345/01-early-life.md
```

### Adding Photos

1. Create directory: `documents/I12345/`
2. Add photo: `photo.jpg`
3. Add caption: `photo.md` (Markdown file with same name)

### Updating Static Pages

Edit files in `content/`:
- `index.md` - Home page
- `pages/about.md` - About page
- `pages/preface.md` - Preface

## 🔄 Updating the Platform

To get the latest features and bug fixes from the platform:

```bash
cd platform
git pull origin main
cd ..
git add platform
git commit -m "Update platform to latest version"
git push origin main
```

## 📄 License

- **Platform code**: MIT License (see platform/LICENSE)
- **Family data**: Copyright © Hoffman Family

## 🙏 Acknowledgments

Built with the [Family History Platform](https://github.com/moshehoff/family_history_platform) by Moshe Hoff.

