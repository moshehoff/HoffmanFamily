# Hoffman Family History

This repository contains the family history website for the Hoffman family, built using the [Family History Platform](https://github.com/moshehoff/family_history_platform).

## 🌐 Live Site

Visit the live site at: https://moshehoff.github.io/HoffmanFamily/

## 📁 Repository Structure

```
HoffmanFamily/
├── platform/                      # Family History Platform (submodule)
├── data/
│   ├── tree.ged                   # Family GEDCOM file
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
├── config/
│   └── family-config.json         # Site configuration
└── .github/
    └── workflows/
        └── deploy.yml             # GitHub Actions deployment
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
python platform/scripts/doit.py data/tree.ged
```

3. **Build the site**:
```bash
cd platform/site
npm install
npx quartz build
```

4. **Preview locally**:
```bash
npx quartz serve
```

Visit http://localhost:8080

## 📝 Making Changes

### Updating Family Data

1. Edit `data/tree.ged` in your genealogy software
2. Export and replace `data/tree.ged`
3. Rebuild: `python platform/scripts/doit.py data/tree.ged`

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

