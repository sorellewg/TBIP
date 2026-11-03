# How to update tbip-scores.org

(Files starting with `_` are ignored by Quarto, so this note is not published.)

## Site layout

| Page | Source file | Notes |
|---|---|---|
| Home | `index.qmd` | Chart is `images/house118.svg` |
| House | `house/index.qmd` | Topic viewer at top, then floor-speech CSVs, then Twitter |
| Senate | `senate/index.qmd` | Floor-speech CSVs |
| Methodology | `methodology/index.qmd` | |
| Menu, footer, site settings | `_quarto.yml` | |
| Fonts, colors, layout | `styles.css` | |

- **CSV files:** `speeches/files/` (floor speeches, House and Senate) and `twitter/files/`. These paths are kept so old download links keep working.
- **Codebook:** `speeches/files/Codebook.pdf`
- **House topic viewer:** `house/topics/NNN_combined.html` (one per Congress) and `house/topics/sessions.js` (the list used by the "Congressional Sessions" menu).
- The old Floor Speeches and Twitter page addresses redirect to the House page (set by `aliases:` in `house/index.qmd`).
- The built site is in `docs/`, which GitHub Pages publishes. Don't edit `docs/` by hand.

## Common updates

**Add or replace a CSV**
1. Put the file in `speeches/files/`, named like `TBIP_119house.csv` or `TBIP_119senate.csv`.
2. Add or edit its row in the table in `house/index.qmd` or `senate/index.qmd`.

**Add a House topic HTML**
1. Put the file in `house/topics/`, named like `119_combined.html` (no " (1)" in the name).
2. Add it to the list in `house/topics/sessions.js`.
3. To show the newest Congress first, change `118_combined.html` to the new file in both places in `house/index.qmd`.

## Publish

In VS Code: **File → Open Folder → TBIP**, then **Terminal → New Terminal** (make sure `quarto preview` isn't running in it; press Ctrl+C if it is).

```
quarto preview      # optional: check it in the browser, Ctrl+C to stop
quarto render
git add -A
git commit -m "Describe the change"
git push
```

Or, after `quarto render`, use the Source Control sidebar: type a message, **Commit**, then **Sync Changes**.
The live site updates a minute or two after pushing. Use Cmd+Shift+R to reload without the cache.

## Open items (Nov 2026)

- **112th House CSV is wrong:** `speeches/files/TBIP_112house.csv` is the same file as the 113th. It needs the real 112th file.
- The old `data/` page is still published at /data, with an outdated citation and a misspelled duplicate, `TBIP_115semate.csv`. It can be removed.
- There's no 110th House topic HTML yet, so it isn't in the viewer menu.
