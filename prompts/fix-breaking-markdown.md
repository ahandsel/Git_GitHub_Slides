# Fix render-breaking Markdown for the Jekyll/GitHub Pages build

You are auditing a Jekyll site published via GitHub Pages' built-in build (deploy-from-branch, `github-pages` gem).
The markdown processor is **Kramdown with GFM input** - NOT GitHub.com's renderer.
Your job is to find and fix Markdown that renders correctly in the GitHub repo preview but breaks on the _published_ Kramdown-built site.


## Step 0 - Confirm the build (do this first, don't assume)

* Read `_config.yml` for `markdown:`/`kramdown:` settings, theme, and plugins.
* Check for a `Gemfile` and `.github/workflows/*` - their absence means the classic GH-Pages Jekyll build (Kramdown).
  If a custom processor/action is configured, adjust the rules below accordingly and say so.
* Note that `pnpm lint` (markdownlint-cli2 + prettier) already handles curly quotes, em/en dashes, NBSP, relative-link validity, and an inline-HTML allowlist.
  DO NOT duplicate those - focus on render-breakers lint misses.


## Step 1 - Scan every tracked `*.md` for these issue classes

Report each hit as `file:line` with the offending snippet.
Categorize:

**A. Pipe `|` in link text or inline content** (HIGH - breaks GFM tables and can mangle anchors)

* `[text | more](url)` and any `|` inside a line that is, or sits adjacent to, a table.
* A `|` inside a heading also corrupts the auto-generated anchor (and any TOC link pointing at it).

**B. Angle-bracket placeholders outside code spans** (HIGH - Kramdown parses `<word>` as a raw HTML tag and silently DROPS it)

* e.g. `use sudo <command>` in prose renders as `use sudo` with `<command>` gone.
  Only flag occurrences NOT already inside backticks or a fenced code block.

**C. Unintended indented code blocks** (MEDIUM) - 4-space/tab-indented lines following a blank line that were meant as prose or nested list content.

**D. Anchor/TOC mismatches** (MEDIUM) - in-page links `[..](#anchor)` whose target heading doesn't produce that exact Kramdown slug (punctuation like `?`/`|` dropped, spaces→ `-`, lowercased, `--` from removed chars).

**E. Raw `<` `>` `&` and bare `{{ }}`/`{% %}`** that Kramdown or Liquid would misinterpret (LOW unless inside front-matter-adjacent content).


## Step 2 - Flag everything

Print a table: `# | file:line | class | snippet | severity | auto-fixable?`


## Step 3 - Auto-fix ONLY the safe, unambiguous cases; leave the rest flagged

Safe to auto-fix:

* **Class A in link text**: replace the separating `|` / `|` with `-`, preserving spacing.
  Example: `[Download | Node.js](url)` → `[Download - Node.js](url)`
  If the `|` is in a heading, also update every TOC/in-page link that targets the old anchor.

NOT safe - flag for human review instead of editing:

* Class B (wrapping in backticks may change intended meaning),
* pipes that are legitimate table delimiters,
* Classes C/D/E.


## Step 4 - Verify

* Re-run the Step-1 scan to confirm fixed cases are gone.
* Run `pnpm lint` (or `pnpm run lint-md`) and confirm no new violations.
* Summarize: what was auto-fixed (with a diff), and a checklist of what still needs human judgment.

Make edits surgically (one precise edit per occurrence).
Do not reformat unrelated lines - prettier/markdownlint own formatting.
