# G80 M3 Car Wash Plan

Interactive car wash checklist and reference guide for an Isle of Man Green BMW M3 G80 (ceramic coated).

## Files

| File | Purpose |
|---|---|
| `wash-plan.json` | **All data** — edit this to add/remove products, steps, tools, dilutions |
| `index.html` | Interactive viewer — reads `wash-plan.json`, renders the full app |
| `REFERENCE.md` | Quick-lookup sheet — dilution ratios, chemical notes, wash sequence overview |

## Usage

### On your phone (GitHub Pages — recommended)
1. In your repo: **Settings → Pages → Deploy from branch → main / root**
2. GitHub will give you a URL like `https://yourusername.github.io/repo-name`
3. Bookmark that URL on your phone — full interactive app, works in Safari/Chrome

### Locally
```bash
cd your-repo-folder
python3 -m http.server 8080
# Open http://localhost:8080 in your browser
```

> **Why a server?** Browsers block local JSON file reads for security. The Python server takes 5 seconds to start and solves this.

### Reference only (offline)
Open `REFERENCE.md` in any markdown viewer — GitHub mobile, Working Copy, Obsidian, iA Writer, etc. All dilution ratios and chemical notes are there without needing a server.

## Making updates

**All edits go in `wash-plan.json`** — the HTML viewer never needs to be touched.

### Add a chemical
```json
{
  "name": "Your Product Name",
  "category": "Category label",
  "modes": ["normal", "maint"],
  "usedOn": "Where you use it",
  "dilutions": [
    {
      "context": "Application context",
      "ratio": "1:10",
      "amount": "100ml per 1L water",
      "note": "Any important notes"
    }
  ],
  "tool": "What tool you use to apply it"
}
```

### Add a wash step
```json
{
  "id": "n19",
  "title": "Step title",
  "desc": "Full description of what to do.",
  "tools": ["Tool 1", "Tool 2"],
  "chems": ["Chemical — dilution"]
}
```
Add to `washSteps.normal` for steps that appear in both modes.  
Add to `washSteps.maintOnly` for maint-only steps, with `"insertAfter": "step_id"`.

### Add a tool
```json
{ "category": "Category", "name": "Tool name", "qty": "1", "usedFor": "What it does" }
```

### Update a dilution
Find the chemical by name in `chemicals[]` and edit its `dilutions` array.

### Update the last-modified date
Edit `meta.lastUpdated` in `wash-plan.json`.

## Wash modes

| Mode | When | Extra steps |
|---|---|---|
| **Bi-weekly normal wash** | Every 2 weeks | Standard 18-step process |
| **Ceramic maintenance** | 2× per year | Adds BH Touchless + Descale before wash, HydrO2 Foam after drying |

## Engine bay clean
Separate optional tab — standalone session only. Engine must be fully cool (2–3 hrs). See the Engine Bay tab in the app or `REFERENCE.md` for the cover/protect list.
