# Workboard

## Current Phase

`vision-architecture-ingest-and-synthesis`

## Phase Goal

Process the currently staged vision-architecture PDFs in `raw/inbox/`, compile them into `wiki/`, integrate AlexNet and dilated convolutions into the current branch structure, and stop only when the resulting branch state is verified and naturally ready for handoff.

## Work Items

### WB-1 Compile `1511.07122v3` into the knowledge base

- Priority: P0
- Depends on: none
- Done definition:
  - `raw/sources/1511.07122v3/1511.07122v3.md` has been interpreted
  - a source summary exists in `wiki/sources/`
  - a concept page exists or is updated in `wiki/concepts/`
  - `wiki/INDEX.md`, `wiki/overview.md`, and `wiki/log.md` reflect the ingestion
- Verification method:
  - `rg -n "1511.07122v3|dilated-convolutions|multi-scale-context-aggregation-by-dilated-convolutions" wiki/INDEX.md wiki/overview.md wiki/log.md wiki/sources wiki/concepts`

### WB-2 Compile the AlexNet paper into the knowledge base

- Priority: P0
- Depends on: none
- Done definition:
  - the AlexNet PDF in `raw/inbox/` has been converted into `raw/sources/`
  - a source summary exists in `wiki/sources/`
  - a concept page exists or is updated in `wiki/concepts/`
  - the branch position of AlexNet is reflected in `wiki/INDEX.md`, `wiki/overview.md`, and `wiki/log.md`
- Verification method:
  - `rg -n "alexnet|imagenet-classification-with-deep-convolutional-neural-networks|deep-convolutional-neural-networks" wiki/INDEX.md wiki/overview.md wiki/log.md wiki/sources wiki/concepts`

### WB-3 Synthesize the dense-prediction architecture branch

- Priority: P0
- Depends on: WB-1
- Done definition:
  - at least one reusable output exists explaining the branch significance
  - at least one `wiki/notes/cases/` page exists that captures the transferable judgment
- Verification method:
  - `rg -n "dense-prediction|classification|dilated-convolutions|vision-architecture" wiki/INDEX.md wiki/log.md wiki/notes/cases outputs`

### WB-4 Refresh the next-step memo for the current vision branch

- Priority: P1
- Depends on: WB-1, WB-2, WB-3
- Done definition:
  - the current branch state is summarized in an output or note that makes the next reading order explicit
  - the branch can be resumed later without rereading all source material
- Verification method:
  - `rg -n "next research directions|vision architecture|next step|reading order" outputs wiki/notes`

## Natural Stop Rule for This Phase

This phase reaches a natural handoff only when:

- WB-1, WB-2, WB-3, and WB-4 are all complete
- all verification methods have passed
- no unresolved high-risk decision remains inside this phase
- continuing would require a new paper selection or a new vision sub-branch decision
