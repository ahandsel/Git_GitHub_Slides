# AGENTS.md

Project-specific rules for AI agents working in this repo.


## What this repo is

This repo holds the content for a short "Intro to Git & GitHub" training course.
It is published as a website via GitHub Pages and is also read directly on GitHub.com.
The upstream project is [ahandsel/Git_GitHub_Slides](https://github.com/ahandsel/Git_GitHub_Slides), and the material is used for Cybozu / Kintone Dojo onboarding.

The content is **bilingual**: Japanese is the primary language and English is the secondary translation.
Some English files are still marked "⚠️ Pending Translation".


## Target audience

The readers are **non-technical members preparing for an upcoming new role** that will require Git.
They are new to Git and to version control in general, and they read in either Japanese or English.
Assume no prior command-line, software-engineering, or Git background.

Write for that reader:

* Choose plain, everyday wording over technical jargon; when a Git term is unavoidable, define it in plain language the first time it appears.
* Explain the "why" behind a step, not just the command to type.
* Keep sentences short and concrete, and prefer a worked example over an abstract description.
* Avoid assuming knowledge of related tools, workflows, or concepts the reader has not been shown yet.
* Keep this tone consistent across both the Japanese and English versions.


## Repository structure

* Lecture and guide content lives in numbered Markdown files at the repo root.
  Each topic has a Japanese file and an English counterpart suffixed `_EN`.
  * `00_Prep.md` / `00_Prep_EN.md` - environment setup (install Git, GitHub account, Desktop app, CLI).
  * `01_Start.md` / `01_Start_EN.md` - Git/GitHub basics, first repo, `git remote`, `git push`.
  * `02_Branches.md` / `02_Branches_EN.md` - creating/merging branches, GitHub workflow, site tour.
  * `03_Revert.md` / `03_Revert_EN.md` - undoing changes.
  * `04_CheatSheet.md` / `04_CheatSheet_EN.md` - Git CLI command reference.
  * `05_CodeReview.md` / `05_CodeReview_EN.md` - submitting Kintone Dojo work as a Pull Request.
* `README.md` (Japanese) and `README_EN.md` (English) are the entry points and link to every lecture.
* `Windows_WSL.md` is a standalone guide for running Git under Windows Subsystem for Linux.
* `Quiz_Answers.md` holds quiz answers, and `English_GitHub_Lec.md` is a combined English lecture draft.
* `img/` holds ~118 screenshots; filenames are prefixed with the lecture they belong to (e.g. `02_Branches_*`).
* `archive/` holds the retired 2021 PowerPoint/PDF version of the course - treat it as read-only history.


## Build and publishing

The site is built by GitHub Pages' built-in Jekyll (deploy-from-branch); there is no `Gemfile` and no GitHub Actions workflow.
The Markdown processor is therefore **Kramdown with GFM input**, NOT GitHub.com's renderer, so content can render differently on the published site than in the repo preview.
See [\_config.yml](_config.yml): theme `jekyll-theme-cayman`, plugin `jekyll-relative-links` (rewrites `*.md` links to relative HTML links), and `README.md` is force-included.

Because of `jekyll-relative-links`, cross-references between docs must use relative `*.md` paths (e.g. `[Prep - 00_Prep.md](00_Prep.md)`), not absolute or `.html` URLs.
A prompt for finding and fixing Kramdown render-breakers lives in [prompts/fix-breaking-markdown.md](prompts/fix-breaking-markdown.md).

Kramdown strips non-ASCII characters when it auto-generates heading IDs, so Japanese headings collapse to `section`, `section-1`, ... and any `#日本語` TOC link that works on GitHub.com breaks on the published site.
Give every heading that contains non-ASCII characters an explicit Kramdown anchor with a short, descriptive ASCII slug (e.g. `## 概要 {#overview}`), and point its in-page TOC link at that slug (e.g. `[概要](#overview)`).
See [01_Start.md](01_Start.md) for the established pattern.


## Tooling and commands

* Package manager is **pnpm** (`>=10`); Node is pinned to `25.4.0` via `.node-version` and required `>=24` with `engine-strict`.
* `pnpm lint` runs the full pass: `prettier --write .` then `markdownlint-cli2 --fix`.
* `pnpm run lint-md` runs only markdownlint, and `pnpm run lint-code` runs only prettier.
* `pnpm test` is an alias for `pnpm lint`.
* `pnpm-workspace.yaml` sets `minimumReleaseAge` to a three-day buffer, so newly published dependency versions are held back for security.


## Style and linting rules

* Markdown is linted by [.markdownlint-cli2.jsonc](.markdownlint-cli2.jsonc).
  Custom `search-replace` rules forbid curly quotes, em dashes, en dashes, non-breaking spaces, and the object-replacement character - use straight quotes and a plain hyphen `-` instead.
  Unordered lists use `*`, nested indent is 2 spaces, and inline HTML is limited to an allowlist (`br`, `pre`, `ul`, `li`, `ol`, `details`, `summary`, `span`).
* Prettier config is [.prettierrc.json5](.prettierrc.json5): 2-space indent, single quotes, with plugins for XML/SVG, shell, SQL, and TOML.
* Spelling is checked by cspell ([.cspell.json](.cspell.json)); add genuinely-correct project terms to its `words` list, and see `words-to-avoid.txt` for the small list of discouraged words it flags.
* `.gitignore` excludes generated artifacts: `/PDF`, `*.pptx`, and `temp.*` - do not commit these.


## Markdown prose style

Write one complete sentence per line.
Do not split a single sentence across multiple wrapped lines, and do not put multiple sentences on one line.
When a sentence belongs to a list item or continues an indented block, keep the continuation sentence on its own line at the same indentation.

This keeps diffs sentence-scoped and easy to review.

Note: `prettier --write` (run via `pnpm lint`) re-wraps prose to a fixed column width and will undo this layout.
Keep files that must follow this rule out of prettier's reach (e.g. add them to `.prettierignore`) or set `"proseWrap": "preserve"`.


## Editing conventions

* Keep Japanese and English files in parity: when you change content in one language, update its `_EN` (or non-`_EN`) counterpart, or note the gap.
* Reference images from `img/` using the lecture-prefixed naming scheme already in use.
* Prefer relative links between docs so the Jekyll build and GitHub view both resolve them.
* When you add or rename a Japanese/non-ASCII heading, give it an explicit `{#ascii-slug}` anchor and update the matching in-page TOC link - see "Build and publishing" for why.
