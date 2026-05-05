---
title: "(8) the rise of the minions - stripe's autonomous agents"
source: "https://www.linkedin.com/pulse/rise-minions-stripes-autonomous-agents-dominik-fretz-cla4c/"
author:
published: 2026年3月5日
created: 2026-04-13
description:
tags:
  - "clippings"
---
stripe is merging 1,300 pull requests a week — all of them initiated by autonomous agents.

about 40% of those PRs merge without a single human edit. the other 60% still need a human to finish the job. but in every case, the agent wrote the branch, ran the tests, fixed what it could, and handed a working starting point to a reviewer. at scale. in production. at a company processing $1 trillion a year.

i read both of stripe's minion posts (\*sources below) last week and i've been thinking about them ever since - because the architecture decisions they made are the same ones i've been working through in my own agent builds. and they got a lot of it right.

here's what the posts actually say, what i think it means, and why it matters for how we build.

**𝘄𝗵𝘆 𝘀𝘁𝗿𝗶𝗽𝗲 𝗯𝘂𝗶𝗹𝘁 𝘀𝗼𝗺𝗲𝘁𝗵𝗶𝗻𝗴 𝗻𝗲𝘄**

stripe's codebase is hundreds of millions of lines across multiple repos. they use Ruby with Sorbet typing — a static type system that most LLMs have barely seen. they have vast proprietary libraries that have never been on the public internet.

their framing: "vibe coding a prototype from scratch is fundamentally different from contributing code to stripe's codebase."

stripe actually uses Cursor and Claude Code heavily — they work closely with both Anthropic and the Cursor team. but those tools are synchronous: they pair with an engineer who is present. what stripe needed was something asynchronous — an agent that could take a task and work independently while the engineer moves on to something else.

that's why they built Minions. the framework it's based on — Goose — actually originated at Stripe. they built it, ran it internally for a year, and then collaborated with Block to open-source it. they didn't grab a third-party tool off the shelf; they were primary architects of the underlying framework.

that's the context. now here's how the system actually works.

**𝘁𝗵𝗲 𝗲𝗻𝗱-𝘁𝗼-𝗲𝗻𝗱 𝗳𝗹𝗼𝘄**

a typical minion run looks like this:

an engineer types a task description into Slack. that's it. no follow-up. no back-and-forth. the minion takes the message, spins up its own isolated environment, does the work, and comes back with a pull request.

but what happens in between those two events is where the real engineering is.

**𝗱𝗲𝘃𝗯𝗼𝘅𝗲𝘀: 𝘁𝗵𝗲 𝗶𝗻𝗳𝗿𝗮𝘀𝘁𝗿𝘂𝗰𝘁𝘂𝗿𝗲 𝗳𝗼𝘂𝗻𝗱𝗮𝘁𝗶𝗼𝗻**

every minion gets its own dedicated AWS EC2 instance — a devbox. not a container. not a lightweight sandbox. the exact same full-fat dev machine a stripe engineer would use.

these devboxes are designed to be "hot and ready" within 10 seconds. stripe achieves this through proactive pooling — they keep a pool of pre-warmed instances running, pre-cloned with the repo, build caches already warm, internal code generation services already running. when a minion request comes in, it picks up a box that's already ready to go.

the consequence of using full devboxes is profound: the agent has the same tools, the same environment, the same feedback loops as a human engineer. there's no impedance mismatch between what the AI does and what CI will do later. if linting passes locally, it passes in CI. no surprises.

and because the devboxes are isolated from production — no real user data, no stripe's production services, no arbitrary network egress — stripe can give the agent full permissions inside them. no confirmation dialogs. no "are you sure?" prompts. the blast radius is structurally contained, so you get clean autonomy without the paranoia.

engineers maintain multiple devboxes simultaneously. spinning up several parallel minions to tackle five tasks at once is normal.

**𝗯𝗹𝘂𝗲𝗽𝗿𝗶𝗻𝘁𝘀: 𝘁𝗵𝗲 𝗵𝘆𝗯𝗿𝗶𝗱 𝗼𝗿𝗰𝗵𝗲𝘀𝘁𝗿𝗮𝘁𝗶𝗼𝗻 𝗽𝗿𝗶𝗺𝗶𝘁𝗶𝘃𝗲**

this is the architectural decision i keep coming back to.

stripe calls their workflow system "blueprints." a blueprint is a state machine that mixes two kinds of nodes:

- **deterministic nodes** (drawn as rectangles): "run configured linters", "push changes", "apply autofixes". no LLM involved. just code that runs reliably every time.
- **agentic nodes** (drawn as cloud shapes): "implement task", "fix CI failures". full LLM autonomy — the agent decides what to do.

you design the blueprint by deciding which steps get deterministic nodes and which get agentic ones. the linting step is always deterministic. the "figure out what's failing and fix it" step is always agentic. you're not choosing between a workflow tool and an agent. you're composing them.

this matters enormously at scale. deterministic steps don't burn tokens. they don't hallucinate. they run fast and cheap. every step you can make deterministic is a step that can't fail in an unexpected way. the agentic steps do the judgment work — which is exactly what LLMs are good at.

stripe lets individual teams write their own custom blueprints for their own workflows. codebase migration? write a blueprint for it. generating boilerplate for a new service? blueprint. the primitive is general-purpose.

**𝗰𝗼𝗻𝘁𝗲𝘅𝘁 𝗴𝗮𝘁𝗵𝗲𝗿𝗶𝗻𝗴: 𝗵𝗼𝘄 𝘁𝗵𝗲 𝗮𝗴𝗲𝗻𝘁 𝗸𝗻𝗼𝘄𝘀 𝘄𝗵𝗮𝘁 𝗶𝘁 𝗻𝗲𝗲𝗱𝘀 𝘁𝗼 𝗸𝗻𝗼𝘄**

before the agent starts writing code, it needs to understand stripe's conventions, patterns, and constraints. this is done two ways.

**rule files.** stripe uses Cursor's rule file format — markdown files that live in the repo and get scoped to specific subdirectories or file patterns. a rule file for the payments module might explain the preferred error handling pattern, which internal libraries to use, what not to do. these are the same rule files that human engineers have authored for Cursor. stripe syncs them across minions, Cursor, and Claude Code so all three tools operate from the same context. one source of truth, shared across every agent.

the scoping is deliberate. you don't inject every rule file into every task. if the agent is touching the payments module, it gets the payments rules. if it's in the API layer, it gets the API rules. context window management isn't an afterthought — it's built into the architecture. global rules that fill the whole context window are explicitly avoided.

**the toolshed and MCP.** stripe built an internal MCP server called Toolshed. it contains nearly 500 tools — integrations with internal systems, SaaS platforms, code intelligence, documentation. but the agent doesn't get all 500. giving an agent 500 tools causes what stripe calls "token paralysis" — the model bogs down trying to figure out which tool to use.

instead, the orchestrator curates a surgical subset of ~15 tools relevant to the task at hand, and that's what the agent gets. engineers can add thematically grouped tool bundles for specific workflows. the security controls are built into the MCP layer — destructive actions are blocked at the tool level, not by relying on the agent's judgment.

**𝘁𝗵𝗲 𝗳𝗲𝗲𝗱𝗯𝗮𝗰𝗸 𝗹𝗼𝗼𝗽: 𝘁𝗵𝗿𝗲𝗲 𝘁𝗶𝗲𝗿𝘀, 𝘁𝘄𝗼 𝗮𝘁𝘁𝗲𝗺𝗽𝘁𝘀, 𝗼𝗻𝗲 𝗵𝗮𝗿𝗱 𝗰𝗮𝗽**

this is where stripe's engineering discipline really shows.

stripe has 3+ million tests. running all of them on every agent iteration would be catastrophically expensive and slow. so the feedback loop is structured as three tiers:

**tier 1 — local linting, under 5 seconds.** before the agent even pushes, a deterministic lint step runs locally. a background daemon pre-computes lint results and caches them so they're fast. the agent catches formatting issues, type errors, obvious style violations immediately and cheaply — before they cost CI time.

**tier 2 — selective CI.** when the agent pushes, CI doesn't run all 3 million tests. it runs only the tests that are relevant to the changed files — a selective subset. where autofixes are available, they're applied automatically. this cuts CI time dramatically while still catching the issues that matter.

**tier 3 — the hard cap.** if a test fails and there's no autofix, the error goes back to the agentic node. the agent gets one attempt to fix it locally, then pushes again. that's it. two CI rounds total. stripe's explicit reasoning: "if the LLM can't fix it in two tries, a third won't help — it just burns compute." after the second push, whatever state the branch is in goes to a human.

this isn't a failure mode. it's a design choice. a minion that gets 80% of the way to a solution is still useful — it's a better starting point for a human than a blank editor. stripe explicitly says incomplete runs are "excellent starting points for focused engineering work."

the cap prevents the failure mode i see in most agent systems: infinite retry loops that spin up cost, burn tokens, and often make things worse with each attempt.

**𝗵𝗼𝘄 𝘀𝘁𝗿𝗶𝗽𝗲 𝗹𝗮𝘂𝗻𝗰𝗵𝗲𝘀 𝗺𝗶𝗻𝗶𝗼𝗻𝘀**

the primary entry point is Slack. the minion can read the full thread context, so engineers can reference earlier conversation, link to tickets, paste error messages. other entry points include a CLI, a web interface, and internal platforms — the feature flag system can trigger a minion directly, the documentation platform can spin one up to update docs, the internal ticketing system automatically creates a minion when a flaky test is detected.

when an engineer is on-call and has ten small issues to fix, they spin up ten minions in parallel. each gets its own devbox. they run simultaneously. the engineer reviews PRs as they come in instead of working sequentially through a queue.

**𝘁𝗵𝗲 𝗻𝘂𝗺𝗯𝗲𝗿 𝘁𝗵𝗮𝘁 𝗱𝗼𝗲𝘀𝗻'𝘁 𝗴𝗲𝘁 𝗲𝗻𝗼𝘂𝗴𝗵 𝗮𝘁𝘁𝗲𝗻𝘁𝗶𝗼𝗻**

part 1 published Feb 9: 1,000+ PRs per week. part 2 published Feb 19: 1,300+ PRs per week.

300 more PRs in ten days. the toolshed grew from 400 tools to 500 in the same window.

that's not a product update cadence. that's a flywheel. each tool added expands what agents can do. each workflow improved makes the next improvement cheaper. stripe didn't just ship a feature — they built a self-improving system.

**𝘄𝗵𝗮𝘁 𝘁𝗵𝗶𝘀 𝗮𝗰𝘁𝘂𝗮𝗹𝗹𝘆 𝗿𝗲𝗾𝘂𝗶𝗿𝗲𝗱**

here's what i think gets missed in the coverage: the agent is not the hard part.

stripe was able to wire agents into their codebase because they had already built:

- devbox infrastructure that gives every engineer a reproducible, isolated environment
- selective CI that can run only the relevant tests for a given change
- sourcegraph for code intelligence and search
- a rich internal tooling ecosystem (Toolshed) that abstracts internal systems into callable APIs
- rule files that document conventions in a machine-readable format

every one of those things was built for human engineers. the agents just used the same infrastructure.

stripe's statement: "our investments in human developer productivity over time have returned to pay dividends in the world of agents."

if your developer infrastructure is flaky, inconsistent, or undocumented — your agents will fail in exactly the same places your engineers struggle. the agents don't fix broken infrastructure. they amplify it, in both directions.

**𝘁𝗵𝗲 𝗽𝗿𝗶𝗻𝗰𝗶𝗽𝗹𝗲 𝘂𝗻𝗱𝗲𝗿𝗻𝗲𝗮𝘁𝗵**

push complexity into deterministic code. let the agent do judgment. keep feedback loops tight and cheap. contain the blast radius by design, then give the agent full trust within that container.

what i see most teams get wrong is the opposite: every step is agentic, the environment is the same one used in production, feedback only comes from a full CI run, and the agent retries indefinitely.

stripe's insight is that the deterministic infrastructure isn't the boring scaffolding you build while waiting to do the real AI work. it IS the real work. the blueprints, the devboxes, the scoped rule files, the curated tool subsets, the hard cap on retries — all of that is deliberate engineering. the agent is the finishing move, not the whole game.

the tools change. the discipline didn't.

**𝘁𝗵𝗲 𝗾𝘂𝗲𝘀𝘁𝗶𝗼𝗻 𝗶'𝗺 𝘀𝗶𝘁𝘁𝗶𝗻𝗴 𝘄𝗶𝘁𝗵**

most teams aren't stripe. you don't have $1 trillion in payment volume justifying a custom agent platform, and you probably shouldn't build one.

but the architecture decisions aren't the expensive part. stripe's expensive investment was the devboxes, the selective CI, the toolshed. if you already have good developer tooling, wiring an agent on top of it is actually not that hard.

the real audit isn't "should we use AI agents?" it's: which parts of our engineering workflow are already reliable enough for an unattended agent to run in? where does our feedback loop take 30 minutes when it should take 30 seconds? which conventions exist only in senior engineers' heads instead of rule files?

stripe spent years building the foundation. the agents showed up and just used it.

what does your foundation look like right now?

---

sources:

*part of my "how i vibe" series on agentic engineering.*