# Lingo 2 — Answer Viewer

A browser-based spoiler tool for [Lingo 2](https://store.steampowered.com/app/2523310/Lingo_2/). Look up any panel by its clue word, see the modifier symbols explained, and reveal answers only when you want them.

---

# Disclaimer

This complete repo (including the README.md you are reading right now) were vibe-coded using [Anthropic Claud](https://claude.ai/new) and while I tried to check everything bugs or errors may be present.

---

## Features

- **Browse by map** — all panels organised into collapsible map groups in the sidebar
- **Search by clue** — find any panel instantly; optionally toggle answer search too
- **Modifier reference** — every symbol rendered using the in-game font, with name and description
- **Multi-modifier support** — chains like `:Rem:Add`, Bar splits like `:Ant|:Rem`, and repeated modifiers like `:Add.` (applied ×2) all display correctly
- **Spoiler answers** — answers are hidden behind a blur by default; click to reveal
- **Hidden-clue panels** — panels where the clue is concealed in-game show the answer plainly and spoiler the hidden clue instead
- **JSON export / import** — export all parsed panels to a single JSON file for fast reloading without the raw game files

---

## Usage

### Option A — Load from JSON (recommended for end users)

If a `lingo2_panels.json` is hosted alongside this page (e.g. on GitHub Pages), visitors can load it directly without touching any game files:

1. Open the viewer
2. Click the **JSON Export** tab on the load screen
3. Either drop the `.json` file onto the page, or paste the hosted URL into the URL field and click **Load from URL**

### Option B — Load from raw game files

This requires extracting the game's `.pck` file first.

#### 1. Extract the game files

Use [gdsdecomp](https://github.com/bruvzg/gdsdecomp) to extract the Lingo 2 `.pck`:

```
gdre_tools --recover-project Lingo2.pck --output-dir ./lingo2_extracted
```

#### 2. Find the `.tscn` scene files

The panel data lives in the extracted scene files in the directory `/objects/scenes/`. Look for files named things like `daedalus.tscn`, `control_center.tscn`, etc.

#### 3. Load into the viewer

1. Open `lingo2_viewer.html` in any modern browser
2. Drop all the `.tscn` files onto the upload area (you can select them all at once)
3. The viewer parses every panel automatically

#### 4. Export for later (optional)

Once loaded, click **Export as JSON** on the home screen. Save the resulting `lingo2_panels.json` — you can load it directly next time without repeating the extraction step.

---

## Hosting on GitHub Pages

1. Fork or clone this repo
2. Add your exported `lingo2_panels.json` to the repo root
3. Enable GitHub Pages (Settings → Pages → Deploy from branch → `main`)
4. Share the Pages URL — visitors can use the **JSON Export** tab and paste the URL to your raw JSON file

The URL for a file hosted on GitHub Pages looks like:
```
https://<your-username>.github.io/<repo-name>/lingo2_panels.json
```

---

## Modifier Reference

The viewer includes a full in-game symbol reference. A summary:

| Symbol | Code | Meaning |
|---|---|---|
| Sun | `:Syn` | Synonym |
| Sun + Bracket | `:Ant` | Antonym |
| Square Bracket (standalone) | `:Brk` | Reverse the word |
| Eye | `:Hom` | Homophone / homonym |
| Eye + Squiggle | `:Rhy` | Rhymes with |
| Hexagons | `:Add` | Add letter(s) |
| Hexagons + Bracket | `:Rem` | Remove letter(s) |
| Hexagons + Squiggle | `:Adp` | Add/remove lines from a letter |
| Box | `:Par` | Clue is part of the answer |
| Box + Bracket | `:Who` | Answer is part of the clue |
| Snowflakes | `:Cat` | Clue is a type of the answer |
| Snowflakes + Bracket | `:Exa` | Answer is a type of the clue |
| Pyramid | `:Int` | Stronger / more intense |
| Pyramid + Bracket | `:Dim` | Weaker / softer |
| Planet | `:Plu` | Plural |
| Planet + Bracket | `:Sin` | Singular |
| Smiley | `:Smi` | Environmental / external clue |
| Smiley + Bracket | `:Sad` | Environmental clue, read right-to-left |
| Smiley + Squiggle | `:Sas` | Search for missing data |
| Spiral | `:Old` | Aged / older form |
| Spiral + Bracket | `:You` | Younger / earlier form |
| Spiral + Squiggle | `:Ten` | Tense change |
| Kerplunk | `:Mas` | Masculine form |
| Kerplunk + Bracket | `:Fem` | Feminine form |
| Empty Set | `:Cha` | Change / transformation |
| Jackhammer | `:Ana` | Anagram |
| Speaker | `:Sou` | Sound made by the clue |
| Speaker + Bracket | `:Sor` | Source of the sound |
| Stars | `:Sur` | Contains / surrounds the clue |
| Stars + Bracket | `:Srr` | Clue contains the answer |
| Cross | `:Ene` | Add energy (heat / charge / kinetic) |
| Cross + Bracket | `:Enr` | Remove energy |
| Rollercoaster | `:Swe` | Sweeten |
| Rollercoaster + Bracket | `:Swu` | Remove sweetness |
| Stethoscope | `:Job` | Action performed by the clue |
| Stethoscope + Bracket | `:Emp` | Who performs the action |
| Salmon | `:Eva` | Cryptic crossword keyword in the clue |
| ? | `:Odd` | Wildcard |

**The Bar (`|`)** splits a symbol string like `:Ant|:Rem` — the clue word is split in two, each half has its symbol applied independently, and the results are recombined.

**Dots** (`:Add.`) mean the modifier is applied more than once — one dot means applied ×2, two dots ×3, and so on.

---

## Files

| File | Description |
|---|---|
| `lingo2_answer_viewer.html` | The viewer — self-contained single file, no dependencies |
| `lingo2_panels.json` | Exported panel data from the game files |

---

## Credits

Symbol definitions based on the community guide [Lingo 2 symbol dictionary](https://steamcommunity.com/sharedfiles/filedetails/?id=3449159664) by Autometalogolex.

In-game font (`Lingo.ttf`) is property of the Lingo 2 developers and is embedded solely for personal display of the original in-game symbols.
