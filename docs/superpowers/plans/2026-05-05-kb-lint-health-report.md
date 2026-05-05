# KB Lint Health Report Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add `scripts/kb lint` to scan broken links, stale wiki pages, and orphan wiki pages, then write a Markdown health report to `outputs/`.

**Architecture:** Extend the existing `scripts/kb` facade with a new `lint` command instead of adding a parallel script. Keep the implementation self-contained inside the shell script: collect markdown files, parse links and `updated:` metadata, compute three issue sets, then render a stable report file and terminal summary.

**Tech Stack:** Bash, `rg`, `find`, `awk`, `sed`, `date`

---

### Task 1: Extend `scripts/kb` usage and command dispatch

**Files:**
- Modify: `scripts/kb`

- [ ] **Step 1: Add `lint` to the usage text**

Update the `usage()` here-doc in `scripts/kb` so it includes:

```text
  scripts/kb lint
```

and the command list entry:

```text
  lint     Scan wiki/ and outputs/ and write a Markdown health report
```

- [ ] **Step 2: Add a `lint)` case arm placeholder**

Add a new `lint)` branch before the final `*)` branch:

```bash
  lint)
    kb_lint
    ;;
```

- [ ] **Step 3: Run the help output**

Run: `scripts/kb`

Expected: usage text now lists `lint` alongside the existing commands.

### Task 2: Implement lint helpers inside `scripts/kb`

**Files:**
- Modify: `scripts/kb`

- [ ] **Step 1: Add path and date helpers above the `case` statement**

Add small helpers for:

```bash
today_iso() { date '+%Y-%m-%d'; }
report_path() { printf '%s/outputs/wiki-health-report-%s.md\n' "$ROOT_DIR" "$(today_iso)"; }
```

and a helper to normalize a repo-relative path:

```bash
to_abs_path() {
  case "$1" in
    /*) printf '%s\n' "$1" ;;
    *) printf '%s/%s\n' "$ROOT_DIR" "$1" ;;
  esac
}
```

- [ ] **Step 2: Add file collection helpers**

Add helpers that emit sorted markdown file lists:

```bash
wiki_markdown_files() {
  find "$ROOT_DIR/wiki" -type f -name '*.md' | sort
}

report_markdown_files() {
  find "$ROOT_DIR/outputs" -type f -name '*.md' | sort
}
```

- [ ] **Step 3: Add a helper for `wiki/INDEX.md` membership**

Implement a helper that checks whether a repo-relative wiki path is mentioned in `wiki/INDEX.md`:

```bash
indexed_in_wiki() {
  local rel_path="$1"
  rg -F --quiet -- "$rel_path" "$ROOT_DIR/wiki/INDEX.md"
}
```

- [ ] **Step 4: Run a syntax check**

Run: `bash -n scripts/kb`

Expected: no output and exit code 0.

### Task 3: Implement the three issue scanners

**Files:**
- Modify: `scripts/kb`

- [ ] **Step 1: Add a broken-link scanner**

Implement a `scan_broken_links` helper that:

- scans `wiki/INDEX.md`, all `wiki/*.md`, and all `outputs/*.md`
- extracts `[label](target)` links
- ignores `http://`, `https://`, `mailto:`, and fragment-only links
- strips `#anchor`
- checks only `.md` targets or absolute local paths ending in `.md`
- prints tab-separated rows:

```text
source-page<TAB>target<TAB>resolved-path<TAB>missing-target
```

- [ ] **Step 2: Add a stale-page scanner**

Implement a `scan_stale_pages` helper that:

- walks `wiki/*.md`
- looks for the first `updated: YYYY-MM-DD`
- compares it with today's date
- emits pages older than 90 days as:

```text
page<TAB>updated-date<TAB>age-days<TAB>stale-page
```

- [ ] **Step 3: Add an orphan-page scanner**

Implement a `scan_orphan_pages` helper that:

- walks `wiki/*.md`
- skips `wiki/INDEX.md`, `wiki/log.md`, and `wiki/overview.md`
- checks whether each repo-relative wiki path appears in `wiki/INDEX.md`
- emits missing ones as:

```text
page<TAB>directory<TAB>suggested-index-section<TAB>orphan-page
```

For `suggested-index-section`, use a simple directory-based mapping such as:

- `wiki/concepts/*` -> `Concepts`
- `wiki/sources/*` -> `Sources`
- `wiki/notes/workflows/*` -> `Notes / 工作流`
- `wiki/notes/frameworks/*` -> `Notes / 框架`
- `wiki/notes/cases/*` -> `Notes / 案例`
- everything else -> `Core or matching section`

- [ ] **Step 4: Run a syntax check again**

Run: `bash -n scripts/kb`

Expected: no output and exit code 0.

### Task 4: Render the Markdown health report

**Files:**
- Modify: `scripts/kb`

- [ ] **Step 1: Add the `kb_lint` renderer**

Implement `kb_lint` so it:

- collects the three issue sets into temp files
- counts each set
- writes `outputs/wiki-health-report-YYYY-MM-DD.md`
- preserves all sections even when a set is empty

The rendered report must contain these headings:

```md
# Wiki Health Report
## Summary
## Broken Links
## Stale Pages
## Orphan Pages
## Suggested Fixes
## Scope Notes
```

- [ ] **Step 2: Add stable empty-state output**

When a section has no findings, render exactly:

```md
无
```

- [ ] **Step 3: Add terminal summary output**

At the end of `kb_lint`, print:

```text
broken links: N
stale pages: N
orphan pages: N
report: /abs/path/to/report.md
```

- [ ] **Step 4: Run the command**

Run: `scripts/kb lint`

Expected: the command prints counts plus a report path and writes the report file under `outputs/`.

### Task 5: Verify against the current repository and document the outcome

**Files:**
- Modify: `README.md`
- Modify: `wiki/notes/workflows/how-to-run-ingest-query-lint-update-in-this-repo.md`
- Modify: `wiki/notes/workflows/index.md`
- Modify: `wiki/INDEX.md`
- Modify: `wiki/log.md`

- [ ] **Step 1: Confirm the generated report structure**

Run:

```bash
sed -n '1,220p' outputs/wiki-health-report-$(date '+%Y-%m-%d').md
```

Expected: the file contains the six required sections and either findings or `无`.

- [ ] **Step 2: Update the docs to mention the executable lint command**

Document that the repo now has `scripts/kb lint` and that it writes a Markdown health report into `outputs/`.

- [ ] **Step 3: Append the repo log entry**

Add a `wiki/log.md` entry describing the new executable lint capability and the health report output.

- [ ] **Step 4: Re-run lint after doc updates**

Run: `scripts/kb lint`

Expected: command still succeeds after documentation changes.

- [ ] **Step 5: Final verification**

Run:

```bash
bash -n scripts/kb
scripts/kb lint
```

Expected:

- `bash -n scripts/kb` exits cleanly
- `scripts/kb lint` exits cleanly and rewrites the report
