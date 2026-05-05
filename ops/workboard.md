# Workboard

## Current Phase

`knowledge-base-governance-consolidation`

## Phase Goal

Align the repository's entry layer, workflow layer, and autonomous-run layer with the knowledge base's current state, so future autonomous runs start from up-to-date metadata, navigation, and protocol boundaries rather than stale phase context.

## Work Items

### WB-1 Refresh top-level repository metadata

- Priority: P0
- Depends on: none
- Done definition:
  - `wiki/INDEX.md` top metadata reflects the true latest update date
  - top-level docs and indices no longer point to stale state
- Verification method:
  - `sed -n '1,12p' wiki/INDEX.md`

### WB-2 Audit workflow and framework linkage

- Priority: P0
- Depends on: none
- Done definition:
  - newly added workflow/framework/case pages are reachable from index or concept/case hubs
  - no obvious high-value orphan remains in the recent governance and harness additions
- Verification method:
  - `rg -n "notes/workflows/index.md|how-to-route-knowledge-queries|how-to-manage-partially-promoted-outputs|how-to-classify-repo-rules|how-to-apply-ops-protocol|agent-harness-engineering" wiki/INDEX.md wiki/notes wiki/concepts`

### WB-3 Reconcile entry-layer rule boundaries

- Priority: P0
- Depends on: WB-1, WB-2
- Done definition:
  - `README.md`, `AGENTS.md`, and `kb-wiki-first` have a stable role split
  - fine-grained rules are routed to workflow guides rather than duplicated into entry files
- Verification method:
  - `rg -n "workflow guides|总原则|wiki/notes/workflows" README.md AGENTS.md .codex/skills/kb-wiki-first/SKILL.md`

### WB-4 Prepare next autonomous branch handoff

- Priority: P1
- Depends on: WB-1, WB-2, WB-3
- Done definition:
  - current governance cleanup status is summarized in outputs or handoff-ready notes
  - the repository can cleanly continue either into governance cleanup execution or a fresh ingest/research branch without rereading all recent changes
- Verification method:
  - `rg -n "governance|workflow|ops|handoff|next step|restart point" outputs wiki/log.md ops/handoff.md`

## Natural Stop Rule for This Phase

This phase reaches a natural handoff only when:

- WB-1, WB-2, WB-3, and WB-4 are all complete
- all verification methods have passed
- entry-layer docs, workflow navigation, and current ops phase context are mutually consistent
- continuing would require a fresh research/ingest decision or a new governance sub-branch
