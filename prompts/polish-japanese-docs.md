# Review and polish the Japanese docs for clarity and consistency

You are proofreading and polishing the **Japanese** source files of a bilingual Git/GitHub training course.
Japanese is the primary language, the audience is beginners, and the tone is instructional.
Your job is to raise the quality of the Japanese prose - clarity, consistency, and correctness - WITHOUT changing meaning, restructuring the lesson, or touching the English `_EN` counterparts.

Read [AGENTS.md](../AGENTS.md) first for repo structure, style, and editing conventions. Follow them exactly.
Note that `pnpm lint` (prettier + markdownlint-cli2) already owns curly quotes, em/en dashes, non-breaking spaces, relative-link validity, list markers, and the inline-HTML allowlist.
DO NOT duplicate those - focus on Japanese-prose quality that linting cannot catch.


## Step 0 - Scope and detect the house conventions (do this first, don't assume)

* List every tracked Japanese (non-`_EN`) `*.md` file at the repo root. These are your only targets.
  * Skip every `_EN` file, `archive/` (retired history), and config/lint/workspace files.
* Before flagging anything, infer the conventions THIS repo already follows by sampling a few files, and treat them as the baseline rather than imposing outside defaults:
  * **Punctuation:** this course uses a half-width comma + space `,` and a half-width period `.` inside Japanese prose (e.g. `Git と GitHub を紹介し, 設定について説明します.`) rather than `、` and `。`. Preserve whichever style a file already uses consistently - do NOT convert `,`/`.` to `、`/`。` or vice versa. Only flag a file that mixes both.
  * **Style (文体):** note whether the file is written in です・ます調 (polite) or である調 (plain). The course is polite throughout.
  * **Spacing:** note the existing spacing around inline ASCII/technical terms (e.g. `Git の基本`).
* If a file's convention is genuinely ambiguous, say so and ask rather than guessing.


## Step 1 - Scan each Japanese file for these issue classes

Report every hit as `file:line` with the offending snippet.
Categorize by severity:

**A. 表記ゆれ - notation inconsistency (HIGH)**

* The same term spelled differently across or within files: katakana variants (`サーバー`/`サーバ`, `ユーザー`/`ユーザ`), okurigana (`行う`/`行なう`), or katakana-vs-English (`コミット`/`commit`, `リポジトリ`/`レポジトリ`).
* Inconsistent casing/spelling of product and command names (`Github`/`GitHub`, `git hub`, `VSCode`/`VS Code`, `Readme`). Build a term table and pick the dominant form as canonical.

**B. 文体の不統一 - mixed politeness (HIGH)**

* です・ます調 and である調 mixed within the same file or section.
* Sentence endings that drift between the two styles in adjacent steps.

**C. Correctness - wrong or confusing Japanese (HIGH)**

* ら抜き言葉 (e.g. `見れる` → `見られる`), 二重否定, and obvious typos / IME misconversions (誤変換).
* Duplicated particles or words (`をを`, `ますます` where unintended), and mismatched brackets `「」（）`.
* Particle (てにをは) errors that change or muddy the meaning.

**D. Clarity and readability (MEDIUM)**

* Overlong sentences (rough guide: one idea per sentence; a single sentence running well past ~100 characters is a candidate to split).
* Redundant phrasing (冗長表現, e.g. `することができます` where `できます` suffices, `〜という`, doubled `の`).
* Weak/uncertain hedging unsuited to instructions (`〜かもしれません`, `〜と思います`) where a direct statement is clearer.
* Long runs of consecutive kanji or repeated conjunctions (`が`, `そして`) that hurt readability.

**E. JP/ASCII spacing and symbols (LOW - confirm lint does not already cover)**

* Inconsistent spacing between Japanese and adjacent half-width ASCII/numerals relative to the file's own pattern.
* Full-width parentheses/spaces or half-width katakana where the file otherwise uses the opposite.
* `!`/`?` and emoji used inconsistently with the rest of the course (the course does use some emoji deliberately - match existing usage, don't strip them).


## Step 2 - Flag everything

Print a table: `# | file:line | class | snippet | suggested fix | severity | auto-fixable?`
For Class A, also print the term table: `term | variants found | canonical choice | # occurrences`.


## Step 3 - Auto-fix ONLY the safe, unambiguous cases; leave the rest flagged

Safe to auto-fix (one surgical edit per occurrence, meaning unchanged):

* Clear typos and IME misconversions, duplicated particles/words, ら抜き, and obvious redundancy (`することができます` → `できます`) where the meaning is unmistakable.
* 表記ゆれ where the canonical form is dominant and uncontested - normalize the minority spellings to it.

NOT safe - flag for human review instead of editing:

* Sentence splits or rewrites that could shift nuance or instructional intent.
* Particle/grammar changes where more than one reading is plausible.
* Any choice of canonical term where the dominant form is unclear - propose, don't impose.
* Anything touching code, CLI commands, file paths, branch names, `git`/`gh` invocations, headings that anchor a TOC, or image alt text tied to a screenshot.

Never edit inside fenced code blocks or inline code spans.
If you fix a heading, also update every in-page `[..](#anchor)` link and the 目次 entry that targets it.


## Step 4 - Verify

* Re-run the Step-1 scan and confirm the auto-fixed cases are gone.
* Run `pnpm lint` and confirm no new violations (note the AGENTS.md caveat: prettier may re-wrap prose, so keep one complete sentence per line).
* Confirm you did not change any code, command, path, or anchor, and that no TOC link is now broken.
* Summarize: what was auto-fixed (with a diff), the term-normalization table you applied, and a checklist of everything still needing human judgment.


## Scope guardrails

* Edit ONLY the Japanese source files. Do NOT touch `_EN` files - if a fix changes meaning, the matching English file may need a follow-up, so flag it for the `sync-en-translations` pass instead of editing it here.
* Preserve the lesson: same headings, same steps, same order, same images. This is a polish pass, not a rewrite.
* Respect the file's existing conventions (punctuation, 文体, spacing) over any external style guide. When a convention is genuinely ambiguous, ask rather than normalize.
