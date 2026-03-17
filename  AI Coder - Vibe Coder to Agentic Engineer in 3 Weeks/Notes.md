# AI Coder: Vibe Coder to Agentic Engineer
**Udemy Course Notes – Edward Donner**
📎 Resources: [edwarddonner.com/2026/02/17/ai-coder-vibe-coder-to-agentic-engineer/](https://edwarddonner.com/2026/02/17/ai-coder-vibe-coder-to-agentic-engineer/)
*Last updated: March 2026*

---

## Table of Contents
1. [AGENTS.md / CLAUDE.md – The Foundation](#1-agentsmd--claudemd--the-foundation)
2. [Evolution of Workflows](#2-evolution-of-workflows)
3. [Pro Techniques – Two Camps](#3-pro-techniques--two-camps)
4. [Claude Code Pro Features](#4-claude-code-pro-features)
5. [Flexible Workflows – Sessions & Checkpoints](#5-flexible-workflows--sessions--checkpoints)
6. [How AI Agents Work – The 4 Tricks](#6-how-ai-agents-work--the-4-tricks)
7. [Three Ways to Give Claude Abilities](#7-three-ways-to-give-claude-abilities)
8. [MCP – Model Context Protocol](#8-mcp--model-context-protocol)
9. [Skills](#9-skills)
10. [Plugins](#10-plugins)
11. [Debugging Strategy](#11-debugging-strategy)
12. [Sandboxing & Remote Execution](#12-sandboxing--remote-execution)
13. [Sub-Agents](#13-sub-agents)
14. [Hooks](#14-hooks)
15. [Code Review & Large Codebases](#15-code-review--large-codebases)
16. [Best Practices](#16-best-practices)
17. [Claude Agent Teams ⭐](#17-claude-agent-teams-)
18. [Agentic Orchestrators – Comparison](#18-agentic-orchestrators--comparison)
19. [Codex (OpenAI)](#19-codex-openai)
20. [Claude Agent SDK & Related Tools](#20-claude-agent-sdk--related-tools)
21. [Deploy on Internet for Free](#21-deploy-on-internet-for-free)
22. [Key Takeaways](#22-key-takeaways)
23. [Quick Reference – Key Links](#23-quick-reference--key-links)

---

## 1. AGENTS.md / CLAUDE.md – The Foundation

### Recommended Template Structure

```markdown
# Project Summary

## Goals
..

## Success Criteria
..

# Code Standards and Guidelines

1. Simpler is better – do not overcomplicate
2. Comments only when necessary
3. Be concise, short README, no emojis
4. IMPORTANT: Avoid overly defensive programming; avoid isinstance checks;
   only manage exceptions when necessary
5. Use uv; ALWAYS `uv run xxx` NEVER `python3 xxx`
```

### 2025 Prevailing Wisdom vs 2026 Mindset

| 2025 Prevailing Wisdom 🟡 | 2026 Mindset 🟣 |
|---|---|
| Invest time crafting AGENTS.md | Let it go |
| AGENTS.md at multiple levels | Focus on end goal |
| Support with supplemental files | More skills |
| Continually rewrite and prune | More loops |
| Often rewrite & reset context | More agents |

### CLAUDE.md Configuration

Update & customize manually in **two locations**:
- `~/.claude/CLAUDE.md` – Global settings (all projects)
- `<project root>/CLAUDE.md` – Project-specific settings

**Contents to include:**
- Overview
- Development process
- AI design
- Technical design
- Colour scheme
- Implementation status:
  - Stages of completion
  - Available API endpoints

**Include files using `@` syntax:**
- Example: in `claude.md` → `@agents.md` → pulls in the contents of `agents.md`

---

## 2. Evolution of Workflows

| Era | Approach | Best For |
|---|---|---|
| 2025 | Micro-manage, Approve, Frequent resets | Mission-critical / large codebase |
| 2025 | Plan, Execute, Review, Test | Mission-critical / large codebase |
| 2025 | SDD – Spec-Driven Design; Trust but verify | Mission-critical / large codebase |
| 2026 | YOLO | MVPs, new builds, boilerplate code |
| 2026 | Ralph Loops | MVPs, new builds, boilerplate code |
| 2026 | Multi-agent swarms, orchestrate | MVPs, new builds, boilerplate code |

> 💡 **Your job is to deliver code that is proven to work.**

---

## 3. Pro Techniques – Two Camps

All pro techniques fall into one of two camps:

| CHAOS 🟣 | CONTROL 🔵 |
|---|---|
| YOLO | Use of files |
| Ralph Loops | Self-correcting |
| GSD | Sandboxes |
| Swarms | Orchestration |

> 🎯 **The goal is controlled chaos.** Driven by project maturity and your comfort level. **Start by prioritising CONTROL.**

---

## 4. Claude Code Pro Features

- `/` Create a Slash Command
- 👥 Multi-Agents and Sub-Agents
- 🏢 Agent Teams
- 🔗 Hooks
- 🔌 Create a Plugin

---

## 5. Flexible Workflows – Sessions & Checkpoints

Two levels of granularity within Claude Code:

| Session (*resume*) | Checkpoint (*rewind*) |
|---|---|
| Resume a previous Claude Code session | Rewind to an earlier state within a session |
| Useful when working across multiple days | Fine-grained undo |
| `/session` command | `Esc` twice to rewind |

In parallel — bulletproof code management: **Git Commits**

> 💡 **Instructor personal workflow:** Git + occasional Checkpointing + Markdown files to record progress. Sessions for exceptional situations (e.g., working over multiple days).

### Slash Commands Reference

| Command | Description |
|---|---|
| `/context` | View current context window |
| `/compact` | Compact the context |
| `/status` | About Claude, usage info |
| `/model` | Switch model |
| `/clear` | Clear conversation history |
| `/stats` | Usage statistics |
| `/permissions` | Manage permissions → `~/.claude/settings-local.json` |
| `/session` | Session management |
| `/remind` | Remind Claude of something |
| `/mcp` | Manage MCP servers |
| `/sandbox` | Enable sandboxing |
| `/hooks` | Configure hooks |

> Tip: Type `/` in Claude Code to see all slash commands instantly.

### Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Shift+Tab` | Alternate between modes |
| `Ctrl+O` | Detailed outputs |
| `Ctrl+C` (twice) | Exit |
| `Esc` (twice) | Rewind |

---

## 6. How AI Agents Work – The 4 Tricks

> Understanding these four tricks demystifies all AI agent behaviour.

### Trick 1: Illusion of Memory
LLMs have no real memory. They simulate it by including prior conversation in the context window. Without context, they can't remember you.

### Trick 2: Reasoning / Thinking
LLMs reason by predicting the best next token. Chain-of-thought prompting helps — the model "thinks out loud" and reaches better conclusions.

### Trick 3: Tools
LLMs can take real-world actions via tools.
- Example: `PYTHON: math.sqrt(math.pi)`
- Claude Code has tools baked in; more tools = more functionality
- This innovation is what enables agents to *act*, not just *generate*

### Trick 4: The Loop
```
Step 1: Ask LLM to make progress
Step 2: Test to see if goal is met
Step 3: If not, go to Step 1
```
This is the core of **all** agentic workflows (Ralph Loop, GSD, Agent Teams, etc.).

---

## 7. Three Ways to Give Claude Abilities

| | MCP 🔌 | Skills 🎯 | Plugins 📦 |
|---|---|---|---|
| **What it is** | Connect Claude Code to someone else's tools | Add expertise & capabilities via Markdown | Convenient bundle of MCP, Skills, Commands & more |
| **Pros** | Massive ecosystem, Highly flexible, Mature marketplaces | Context efficiency, Simple setup, Strong results | Best of both, Simplest setup, Explicit instructions |
| **Cons** | Context hog, Complex setup | Limited flexibility, Still immature | Only Claude Code, Don't over-use |
| **When** | Need 3rd-party tool integration | Need lightweight expertise added | Starting out – **default choice** |

> 🚀 **Recommendation: START WITH PLUGINS.** Most of the time, plugins are the right first choice. Add specific Skills and MCP as needed.

---

## 8. MCP – Model Context Protocol

### What MCP Is and What It's Not

✅ **It IS:**
- Easy way to use Tools written by someone else
- Easy way to share your Tools with others
- Easy way to connect LLMs with Tools
- The game-changer is the **ADOPTION**

❌ **It's NOT:**
- The tools themselves (it's the interface)
- A major innovation (it's an agreed standard)
- Efficient at scale – overuse fills context window → poor results
- The future: Skills may eventually replace MCP for many use cases

### MCP Technicalities

| MCP Host | MCP Client | MCP Server |
|---|---|---|
| Claude Code | Inside Claude Code | The tools written by someone else |

**Transport options (where tools run):**
- **Local** – Code retrieved remotely, runs on your machine. Most common.
- **Remote** – SSE (legacy) or Streamable HTTP

> ⚠️ **Common confusion:** "Local" = where tools *RUN*, not where code lives. A local tool still makes remote API calls. Local has all MCP benefits; the code runs on your box.

### MCP Marketplaces
- `mcp.so`
- `glama.ai`
- `smithery.ai`

### Notable MCP Servers

**context7** – Up-to-date API documentation
```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
```

**GitHub** – Remote transport
```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp \
  --header "Authorization: Bearer YOUR_PAT"
```

**Jira (Atlassian)** – Remote MCP
```bash
claude mcp add --transport http atlassian https://mcp.atlassian.com/v1/mcp
```

**polygon / massive** – Access to stock prices

Remove a server:
```bash
claude mcp remove <name>
# or use /mcp
```

---

## 9. Skills

Introduced after MCP. Primarily focused on **instructions as Markdown files** rather than Tools.

✅ **Advantages:**
- Lightweight and simple – anyone can make them
- "Progressive disclosure" reduces context overhead
- Supports running scripts locally – an interesting alternative type of tool
- Easy to make and share

❌ **Limitations:**
- Not as flexible and powerful as Tools
- Discovery is a Wild West; usually install as Plugin
- Triggering a skill is ad-hoc

> 💡 Skills feel like the more compelling solution for Claude Code, but this is evolving. Skills may replace MCP over time.

### 3 Levels of Progressive Disclosure

| Metadata | Instructions | Resources + Code |
|---|---|---|
| Name + description: When should this skill be triggered? | Information with workflows, guidance, code snippets | Info that can be accessed & scripts that can be run |
| → In `SKILL.md` file | → In `SKILL.md` file | → In other referenced files |

### File System Architecture

Skills use a file system architecture:

```
.claude/
  skills/
    my-great-skill/
      SKILL.md
      more_stuff_here_referenced_above.md
      and_more_stuff.md
      scripts/
        scripts_in_any_language_with_instructions_above.py
```

> 💡 **The script itself stays out of context** — only loaded when the skill is triggered. This is the key efficiency advantage.
> This structure can be in your **home directory** (all projects) or **project directory** (project only).

### skills.sh Commands
```bash
find-skills        # Browse available skills
agent-browser      # Install agent browser skill
skill-create       # Create a new skill
```

**Install Agent Browser skill:**
```bash
npm install -g agent-browser
agent-browser install
npx skills add https://github.com/vercel-labs/agent-browser --skill agent-browser
```

**Useful debugging skill:** `https://skills.sh/obra/superpowers/systematic-debugging`

---

## 10. Plugins

The **highest-level construct**. A bundle of features that can include MCP Servers, Skills, Commands, along with other Claude Code features not yet covered.

✅ **Advantages:**
- The most simple
- Best trade-offs of context and capability
- Commands are explicitly triggered

❌ **Limitations:**
- Only available in Claude Code
- Least configuration flexibility
- May give more functionality than needed

> 🚀 **Most of the time, start with Plugins!** It is the recommended starting point for adding capabilities to Claude Code.

### Custom Plugin File Structure
```
reviewer/
  .claude-plugin/
    plugin.json
    marketplace.json     ← for publishing to marketplace
  /hooks/
    hooks.json
  /skills/
```

**To publish:** use `/plugin` command and add local folder into marketplace. Can also publish to git.

### Custom Commands
```
.claude/commands/    → Custom commands invoked with /command-name
```

### Custom Sub-Agents
```
.claude/agents/      → Custom sub-agent defined in *.md file
```
- Run in background for specific tasks
- Doesn't pollute the current context window
- Can call a different LLM

---

## 11. Debugging Strategy

**Three-step approach:**

### Step 1: Snapshot
Do a **git commit** to save your current state before debugging.

### Step 2: Paste the Trace
Paste the error trace into Claude and let it figure out the cause.

### Step 3: Guide with `debug.md`
```
1. Reproduce consistently
2. Investigate, hypothesis
3. Demonstrate root cause
4. Fix and prove
5. Lessons learned → update CLAUDE.md
```

**Or use a dedicated Skill:** `https://skills.sh/obra/superpowers/systematic-debugging`

---

## 12. Sandboxing & Remote Execution

Two related concepts:

| Sandboxing 🟣 | Remote Execution 🔵 |
|---|---|
| More secure | More work in parallel |
| More productive | Already sandboxed |
| Avoid approval fatigue | Work on the go |

> Evolving space with multiple offerings. Claude Code and Codex have a similar menu of options.

### 3 Main Sandbox Approaches

| Approach | How | Runs On |
|---|---|---|
| **Native Sandbox** | Built into Claude Code, triggered by `/sandbox` | Your machine |
| **Managed Cloud Sandbox** ("Claude Code on the Web") | Via `&` or `claude --remote`; via `@claude` tag in GitHub (needs GitHub app installed); includes `/teleport` and `/tasks` | Anthropic cloud |
| **Third-Party Cloud Sandbox** | Isolated environment on cloud, suitable for all Coding Agents. e.g. `sprites.dev` | Third-party cloud |

### GitHub Integration
```bash
/install-github-app
```
- Create an issue → tag `@claude` with instruction prompts
- → Automatically spawns Claude and implements the issue

### Bypass Permissions
```bash
claude --dangerously-skip-permissions   # Use with caution!
```

---

## 13. Sub-Agents

Sub-agents run in the background with their own context window, keeping the main context clean.

✅ **Advantages:**
- **Parallelism** – accelerate by working on different components at the same time
- **Self-correction** – keep project on rails with agents that check and test
- **Context efficiency** – keep context unpolluted with information related to other tasks
- **Task focus** – keep bounded responsibility and prompts to each agent, reducing context switching

❌ **Limitations:**
- **Orchestration complexity** – more moving parts
- **Boundary issues** – mistakes in the dependencies between agents
- **Error amplification** – mistakes can compound leading to unreliable outcomes... or chaos!
- **Costs** – tokens can add up

### File Structure
```
.claude/agents/          → Custom sub-agent defined in *.md file
```
Example: `change-review.md` – runs a review sub-agent after changes

---

## 14. Hooks

Hooks are triggered when something happens/is completed in Claude:
- As soon as a **tool call** is done
- As soon as a **commit** is done
- As soon as **CLAUDE.md** is updated

```bash
/hooks    # Configure hooks however you want
```

---

## 15. Code Review & Large Codebases

### Code Review Setup
Create a `code-review.md` file with:
- Instructions for what to review
- Fix issues
- Test requirements

### Tips for Large Codebase & Large Team
- **Detailed AGENTS.md and other docs**
- **Consistent workflows / plugins**
- **Special skills for project techniques**
- **Good tests that don't over-mock** – test actual functionality, not just for the sake of testing
- **Human reviewer; reject slop**
- **Always work with small improvements, piece by piece** – don't refactor the whole codebase

---

## 16. Best Practices

- Use the **`feature-dev`** plugin from official Claude plugins
- Update `CLAUDE.md` whenever a new feature is implemented
- `/clear` – Clear context window before next feature
  - ⚠️ Before doing this: ensure new features are updated in `CLAUDE.md`
- Use `/sandbox` for safe experimentation
- **Skills over others** – Skills are reusable across platforms
- Use **Codex** to review Claude's work as a cross-check
- Write detailed business requirements + clear architectural guidelines in `CLAUDE.md` for full capability

---

## 17. Claude Agent Teams ⭐

📎 Docs: [code.claude.com/docs/en/agent-teams](https://code.claude.com/docs/en/agent-teams)

### What They Are
- Coordinate multiple Claude Code instances
- One acts as the **Team Lead**, assigning tasks
- Team-mates work and **interact independently**

### When to Use Them
- Parallel research; debug with different hypotheses
- Own independent modules
- Own different layers (frontend, backend, etc.)

### Agent Teams vs Sub-Agents

| | Sub-Agents | Agent Teams |
|---|---|---|
| **Context** | Own context window; results return to caller | Own context window; fully independent |
| **Communication** | Report results back to the main agent only | Teammates message each other directly |
| **Coordination** | Main agent manages all work | Shared task list with self-coordination |
| **Best for** | Focused tasks where only the result matters | Complex work requiring discussion and collaboration |
| **Token cost** | Lower: results summarised back to main context | Higher: each teammate is a separate Claude instance |

> Use **sub-agents** when you need quick, focused workers that report back. Use **agent teams** when teammates need to share findings, challenge each other, and coordinate on their own.

### Setup Instructions

**Step 1:** Add to `settings.json`:
```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  },
  "teammateMode": "in-process"
}
```

**Step 2:** Prompt Claude: *"Create an agent team to..."*

**Step 3:** `Shift+Tab` to delegate mode; also say:
> *"Wait for your teammates to complete their tasks before proceeding"*

**Step 4:** `Shift+Up/Down` to select team-mate

**Step 5:** Commands to stop when complete:
> *"Ask the researcher teammate to shut down"*
> *"Clean up the team"*

> ⚠️ **Invest in CLAUDE.md; expect cost; be willing to start over.**

### Example Agent Team Prompt

```
Create an Agent Team to complete the project as defined.
Team members:
- Front-end engineer (frontend)
- Backend API Engineer (backend)
- Database Engineer (all DB related code)
- LLM Engineer (LLM calls)
- Integration Tester (builds and runs end-to-end Playwright tests,
  reports issues back to team members)
- DevOps engineer (Docker container and scripts)

All team-members should work on unit tests.
```

---

## 18. Agentic Orchestrators – Comparison

| Orchestrator | Character | Speed |
|---|---|---|
| **GSD** | Reliable | Slow |
| **Claude Agent Teams** | Experimental | Faster |
| **Gas Town** | Chaotic | Fastest |
| **Codex Sub-agents** | Alternative approach | – |

### GSD – Get Shit Done
- GitHub: `gsd-build/get-shit-done`
- Spec-Driven Design meets Multi-Agent Orchestration
- Thorough, but consumes more time & tokens
- Reliable output; similar in delivery to agent-teams

### Gas Town
- GitHub: `steveyegge/gastown`
- Fastest but most chaotic
- Optional extra – involves some chaos!

---

## 19. Codex (OpenAI)

Install: [developers.openai.com/codex/cli/](https://developers.openai.com/codex/cli/)

```bash
codex exec "<Prompt>"   # Run just one task
codex                   # Launch interactive CLI
codex --yolo            # Auto-approve mode (use with caution!)
```

Use Codex to **review Claude's work** as a cross-check.

---

## 20. Claude Agent SDK & Related Tools

### Claude Agent SDK
- Docs: [platform.claude.com/docs/en/agent-sdk/overview](https://platform.claude.com/docs/en/agent-sdk/overview)
- Do all that Claude Code does, but **using code** (programmatic API)

### Claude Cowork
- Link: [claude.com/product/cowork](https://claude.com/product/cowork)
- Download app → Interact with folders & items in your computer
- Example: organize a folder → read all files and create a summary file

### OpenClaw
- Link: [openclaw.ai](https://openclaw.ai)
- Install, configure LLM key, choose any platform, setup for interaction (Telegram, WhatsApp, etc.)

---

## 21. Deploy on Internet for Free

- **fly.dev / fly.io** – Free internet deployment
- **sprites.dev** – Third-party sandbox from fly.io (also supports remote Claude execution)

---

## 22. Key Takeaways

**Pick the Coding Agent & Workflow based on:**
- Project Maturity & Risk Appetite
- Your skills
- Your preference

**Follow these steps:**
1. Pick the plugins that work for you
2. Add specific Skills (and MCP as needed)
3. Trial & error; discard often
4. Use git
5. Use markdown docs

> 🏆 **You own the code you deliver; never push slop.**

---

## 23. Quick Reference – Key Links

| Tool / Resource | Link |
|---|---|
| Course Resources | [edwarddonner.com/2026/02/17/ai-coder-vibe-coder-to-agentic-engineer/](https://edwarddonner.com/2026/02/17/ai-coder-vibe-coder-to-agentic-engineer/) |
| Claude Agent SDK | [platform.claude.com/docs/en/agent-sdk/overview](https://platform.claude.com/docs/en/agent-sdk/overview) |
| Claude Agent Teams | [code.claude.com/docs/en/agent-teams](https://code.claude.com/docs/en/agent-teams) |
| Claude Code (web) | [claude.ai/code](https://claude.ai/code) |
| Claude Cowork | [claude.com/product/cowork](https://claude.com/product/cowork) |
| OpenClaw | [openclaw.ai](https://openclaw.ai) |
| GSD | [github.com/gsd-build/get-shit-done](https://github.com/gsd-build/get-shit-done) |
| Gas Town | [github.com/steveyegge/gastown](https://github.com/steveyegge/gastown) |
| sprites.dev | [sprites.dev](https://sprites.dev) |
| MCP – mcp.so | [mcp.so](https://mcp.so) |
| MCP – glama.ai | [glama.ai](https://glama.ai) |
| MCP – smithery.ai | [smithery.ai](https://smithery.ai) |
| Skills Marketplace | [skills.sh](https://skills.sh) |
| Systematic Debugging Skill | [skills.sh/obra/superpowers/systematic-debugging](https://skills.sh/obra/superpowers/systematic-debugging) |
| Claude Plugins Official | [github.com/anthropic/claude-plugins-official](https://github.com/anthropic/claude-plugins-official) |
| Codex CLI | [developers.openai.com/codex/cli/](https://developers.openai.com/codex/cli/) |
| FinAlly project repo | [github.com/ed-donner/finally](https://github.com/ed-donner/finally) |
| CommonPaper (legal docs) | [commonpaper.com](https://commonpaper.com) |

---
*Notes compiled from handwritten pages + course materials provided.*
