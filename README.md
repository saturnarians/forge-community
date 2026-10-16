# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `npm install`
- `npm run dev`
- visit <http://localhost:3030>

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev at the [documentation](https://sli.dev/).

Use a separate file for each session. Don't put them in `slides.md`, because Slidev treats everything in one file as a single deck, so Sessions 1 and 2 would become one long presentation.

**Recommended layout in `forge_community`:**
```
forge_community/
├── session-01-intro.md
├── session-02-rendering.md
├── demo-reference.md      (the old starter, delete it later)
├── package.json
└── node_modules/
```

**Setup on Fedora:**
```bash
cd ~/path/to/forge_community
mv slides.md session-01-intro.md      # paste Session 1 content into this file
nano session-02-rendering.md          # paste Session 2 content here
```
If you already pasted Session 1 into `slides.md`, the `mv` command just renames it. If you haven't yet, run `nano session-01-intro.md` and paste it there.

**Run a specific session:**
```bash
npx slidev session-01-intro.md
npx slidev session-02-rendering.md
npx slidev session-03-state-data.md
npx slidev session-04-state-data.md
```

**Shortcuts:** add these under `"scripts"` in `package.json`:
```json
"s01": "slidev session-01-intro.md",
"s02": "slidev session-02-rendering.md"
```
Then run `npm run s01` or `npm run s02`.

**One thing to avoid:** `npm run dev` only opens `slides.md`. Once you've renamed it, that command will fail or show an error, so use your `s01` and `s02` shortcuts instead. If you'd rather keep `npm run dev` working, keep your current session as `slides.md` and rename it when the session is done. I'd still use numbered files from the start.

**Why and trade-off:** one file per session gives you a clean, dated history in git, which is useful evidence later, and lets you present or export each session on its own. The cost is a few extra commands, which the shortcuts remove.