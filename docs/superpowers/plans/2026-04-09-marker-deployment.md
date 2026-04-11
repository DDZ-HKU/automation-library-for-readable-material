# Marker Deployment Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Deploy the local `marker` PDF-to-Markdown tool in this workspace and add one reusable command that converts a PDF from `raw/inbox/` into Markdown under `raw/sources/`.

**Architecture:** Keep `marker/` as an isolated Python tool with its own virtual environment and dependencies, then add a thin wrapper script in the knowledge-base workspace that validates inputs and calls `marker_single` with a fixed output location. Verify both tool-level and end-to-end conversion behavior before considering the deployment usable.

**Tech Stack:** Python 3.10+, `venv`, `pip`, `marker-pdf`, shell wrapper script, local filesystem

---

## File Structure

- Create: `docs/superpowers/plans/2026-04-09-marker-deployment.md`
- Create: `scripts/pdf-to-md`
- Create: `marker/.venv/` (local virtual environment, generated)
- Modify: `README.md`
- Use for verification: `raw/inbox/`
- Use for output: `raw/sources/`

### Task 1: Verify and prepare a Python 3.10+ runtime for `marker`

**Files:**
- Modify: none
- Create: none
- Test: runtime commands only

- [ ] **Step 1: Verify which Python versions are available**

Run:

```bash
python3 --version
python3.10 --version
python3.11 --version
python3.12 --version
```

Expected:
- `python3` may be lower than 3.10
- At least one `python3.10+` command must succeed

- [ ] **Step 2: Stop if no supported Python is available**

Decision rule:

```text
If none of python3.10/python3.11/python3.12 exists, do not continue installation.
Report: "marker requires Python 3.10+, but this machine currently does not expose a supported interpreter on PATH."
```

- [ ] **Step 3: Select one interpreter and record it for all later commands**

Recommended command if available:

```bash
python3.11 --version
```

Expected:
- Output similar to `Python 3.11.x`

- [ ] **Step 4: Verify that `venv` works on the selected interpreter**

Run:

```bash
python3.11 -m venv --help
```

Expected:
- Help output prints and command exits successfully

### Task 2: Create an isolated virtual environment inside `marker/`

**Files:**
- Create: `marker/.venv/`
- Modify: none
- Test: `marker/.venv/bin/python`

- [ ] **Step 1: Remove any stale partial environment only if it was created by this task and is broken**

Run:

```bash
test -x marker/.venv/bin/python || true
```

Expected:
- Either the interpreter exists, or the command exits cleanly without deleting user data

- [ ] **Step 2: Create the virtual environment**

Run:

```bash
python3.11 -m venv marker/.venv
```

Expected:
- `marker/.venv/bin/python` is created

- [ ] **Step 3: Verify the virtual environment interpreter version**

Run:

```bash
marker/.venv/bin/python --version
```

Expected:
- Output is `Python 3.10+`

- [ ] **Step 4: Upgrade packaging tools in the virtual environment**

Run:

```bash
marker/.venv/bin/python -m pip install --upgrade pip setuptools wheel
```

Expected:
- `pip`, `setuptools`, and `wheel` install or upgrade successfully

### Task 3: Install `marker` into the isolated environment

**Files:**
- Modify: none
- Create: generated site-packages inside `marker/.venv/`
- Test: `marker/.venv/bin/marker_single`

- [ ] **Step 1: Install the local project in editable mode**

Run:

```bash
marker/.venv/bin/pip install -e /Users/ddz/Documents/exp/marker
```

Expected:
- Installation completes without dependency resolution errors

- [ ] **Step 2: Verify the CLI entry points exist**

Run:

```bash
ls marker/.venv/bin/marker_single
ls marker/.venv/bin/marker
```

Expected:
- Both files exist

- [ ] **Step 3: Verify the single-file CLI can start**

Run:

```bash
marker/.venv/bin/marker_single --help
```

Expected:
- Help text prints without Python import errors

- [ ] **Step 4: Capture the first real blocker if installation fails**

Failure handling:

```text
If pip fails because of network access, package download, or model bootstrap, capture the exact failing package or URL and request escalation only for that install command.
```

### Task 4: Add a stable wrapper command in the knowledge-base workspace

**Files:**
- Create: `scripts/pdf-to-md`
- Modify: none
- Test: `scripts/pdf-to-md`

- [ ] **Step 1: Write the failing usage test mentally from the command contract**

Required behaviors:

```text
scripts/pdf-to-md /abs/or/relative/path/to/file.pdf
- fails if the file does not exist
- fails if the input is not a .pdf
- ensures raw/sources exists
- calls marker/.venv/bin/marker_single with --output_dir raw/sources
```

- [ ] **Step 2: Create the wrapper script with strict error handling**

Write this file to `scripts/pdf-to-md`:

```bash
#!/usr/bin/env bash
set -euo pipefail

ROOT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")/.." && pwd)"
MARKER_BIN="$ROOT_DIR/marker/.venv/bin/marker_single"

if [ "$#" -ne 1 ]; then
  echo "Usage: scripts/pdf-to-md <path-to-pdf>" >&2
  exit 1
fi

INPUT_PATH="$1"

if [ ! -f "$INPUT_PATH" ]; then
  echo "Input file not found: $INPUT_PATH" >&2
  exit 1
fi

case "$INPUT_PATH" in
  *.pdf|*.PDF) ;;
  *)
    echo "Input file must be a PDF: $INPUT_PATH" >&2
    exit 1
    ;;
esac

if [ ! -x "$MARKER_BIN" ]; then
  echo "marker is not installed. Expected executable at: $MARKER_BIN" >&2
  exit 1
fi

mkdir -p "$ROOT_DIR/raw/sources"

"$MARKER_BIN" "$INPUT_PATH" --output_dir "$ROOT_DIR/raw/sources"

echo "Conversion complete. Output written under: $ROOT_DIR/raw/sources"
```

- [ ] **Step 3: Make the wrapper executable**

Run:

```bash
chmod +x scripts/pdf-to-md
```

Expected:
- `scripts/pdf-to-md` is executable

- [ ] **Step 4: Verify the wrapper usage message**

Run:

```bash
scripts/pdf-to-md
```

Expected:
- Exit code is non-zero
- Output contains `Usage: scripts/pdf-to-md <path-to-pdf>`

- [ ] **Step 5: Verify missing-file handling**

Run:

```bash
scripts/pdf-to-md raw/inbox/does-not-exist.pdf
```

Expected:
- Exit code is non-zero
- Output contains `Input file not found`

### Task 5: Verify end-to-end conversion with a real PDF

**Files:**
- Use: `raw/inbox/<sample>.pdf`
- Create: `raw/sources/<sample>/...` or `raw/sources/<sample>.md` depending on marker output
- Test: wrapper command and resulting Markdown

- [ ] **Step 1: Select one real sample PDF already present in the workspace**

Run:

```bash
find raw/inbox -maxdepth 1 -type f \( -name '*.pdf' -o -name '*.PDF' \) | head -n 1
```

Expected:
- One PDF path is returned

- [ ] **Step 2: Stop and report if no sample PDF exists yet**

Decision rule:

```text
If no PDF exists in raw/inbox, deployment can still be considered installed but not fully verified. Ask the user to drop one sample PDF into raw/inbox for end-to-end validation.
```

- [ ] **Step 3: Run the wrapper on the sample PDF**

Run:

```bash
scripts/pdf-to-md "raw/inbox/SAMPLE.pdf"
```

Expected:
- Command exits successfully
- `raw/sources/` receives marker output

- [ ] **Step 4: Inspect the generated output tree**

Run:

```bash
find raw/sources -maxdepth 2 -type f | sort
```

Expected:
- At least one new Markdown file appears

- [ ] **Step 5: Inspect the top of the generated Markdown**

Run:

```bash
sed -n '1,80p' raw/sources/SAMPLE.md
```

Expected:
- Markdown is readable and plausibly derived from the source PDF

### Task 6: Document the workflow for future use

**Files:**
- Modify: `README.md`
- Test: readback only

- [ ] **Step 1: Add a short "PDF to Markdown" section to the repository README**

Append a section like this near the workflow guidance:

```md
## PDF to Markdown

This workspace uses the local `marker/` tool to convert PDFs before they are ingested into the wiki.

Basic flow:

1. Put a PDF in `raw/inbox/`
2. Run `scripts/pdf-to-md raw/inbox/<file>.pdf`
3. Confirm the Markdown appears under `raw/sources/`
4. Then ingest the new Markdown into `wiki/`
```

- [ ] **Step 2: Read back the README section**

Run:

```bash
rg -n "PDF to Markdown|scripts/pdf-to-md|raw/inbox|raw/sources" README.md
```

Expected:
- The new workflow lines appear in `README.md`

### Task 7: Final verification and handoff

**Files:**
- Modify: none
- Test: command checks only

- [ ] **Step 1: Re-run the CLI help through the installed environment**

Run:

```bash
marker/.venv/bin/marker_single --help
```

Expected:
- Help output prints successfully

- [ ] **Step 2: Re-run the wrapper on the verified sample if available**

Run:

```bash
scripts/pdf-to-md "raw/inbox/SAMPLE.pdf"
```

Expected:
- Conversion succeeds a second time without manual environment tweaks

- [ ] **Step 3: Summarize exact deployment outcome**

Report:

```text
- selected Python interpreter
- whether marker installed successfully
- wrapper script path
- one verified sample PDF path, if available
- one generated Markdown path, if available
- any remaining blockers (for example missing Python 3.10+ or no sample PDF)
```
