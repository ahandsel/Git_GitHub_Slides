# Ensure every Japanese doc has an English counterpart

You are auditing a **bilingual** training-course repo where Japanese is the primary language and English is the secondary translation.
Each topic has a Japanese file and an English counterpart suffixed `_EN` (e.g. `01_Start.md` / `01_Start_EN.md`).
Your job is to confirm every Japanese doc has a complete, up-to-date English counterpart - and where one is missing or stubbed, generate it from the existing Japanese content.

Read [AGENTS.md](../AGENTS.md) first for repo structure, style, and editing conventions. Follow them exactly.


## Step 0 - Build the pairing map (do this first, don't assume)

* List every tracked `*.md` at the repo root.
* Pair each Japanese (non-`_EN`) file with its `_EN` counterpart by filename.
  * `README.md` pairs with `README_EN.md`.
  * Standalone or combined drafts (`Windows_WSL.md`, `English_GitHub_Lec.md`, `Quiz_Answers.md`) may not follow the pattern - note them but do not invent pairings.
* Files under `archive/` are retired history - treat as read-only and skip.


## Step 1 - Classify each pair

For every Japanese file, classify its English counterpart as one of:

* **MISSING** - no `_EN` file exists.
* **STUB** - the `_EN` file exists but is near-empty, a placeholder, or marked "⚠️ Pending Translation".
* **STALE** - the `_EN` file exists but is missing sections/headings/images present in the Japanese, or is materially shorter than the content warrants (compare heading structure and image references, not just byte count).
* **IN PARITY** - headings, structure, links, and `img/` references all correspond.

Report a table: `# | JP file | EN file | status | what's missing`.


## Step 2 - Generate the missing English content

For every MISSING, STUB, or STALE pair, write or complete the `_EN` file by translating from the Japanese source:

* **Translate the prose** into natural, instructional English aimed at the same beginner audience. Do not translate literally - convey meaning the way a native English technical writer would for a Git/GitHub intro course.
* **Preserve structure 1:1**: same heading hierarchy, same list/step order, same number of sections. The reader of either language should follow the same flow.
* **Do not translate** code, CLI commands, file paths, branch names, or `git`/`gh` invocations - copy them verbatim.
* **Keep image references** pointing at the same `img/` files (the lecture-prefixed names are language-neutral). Translate alt text and captions only.
* **Rewrite cross-doc links** to point at the English counterpart where one exists (e.g. a JP link to `02_Branches.md` becomes `02_Branches_EN.md` in the EN file). Use relative `*.md` paths so `jekyll-relative-links` resolves them - never `.html` or absolute URLs. If the target has no `_EN` file yet, link to the Japanese file and flag it.
* **Remove the "⚠️ Pending Translation" marker** once the file is genuinely translated.

Apply repo prose style: one complete sentence per line, `*` for unordered lists with 2-space nested indent, straight quotes, plain hyphen `-` (never curly quotes, em/en dashes, or NBSP), and inline HTML only from the AGENTS.md allowlist.


## Step 3 - Verify

* Re-run the Step-1 classification and confirm every pair you touched is now IN PARITY.
* Run `pnpm lint` and confirm no new violations (note: prettier may re-wrap prose - see the AGENTS.md caveat on the one-sentence-per-line rule).
* Confirm every relative `*.md` link in the new content resolves to an existing file.
* Summarize: which `_EN` files were created or completed, a diff or heading outline for each, and a checklist of anything left for human review (e.g. links whose `_EN` target doesn't exist yet, or content that needs a subject-matter check).


## Scope guardrails

* Do NOT edit the Japanese source files - they are the source of truth. Only create/complete `_EN` files.
* Do NOT generate an `_EN` file for something that isn't a translatable Japanese doc (config, lint, workspace files).
* If a Japanese file is itself incomplete, translate what exists and flag the gap rather than inventing material.
