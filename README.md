# SCALE AI Foundation Skills

Join 500+ creative agencies, DTC brands, and performance marketing teams inside SCALE AI: https://www.skool.com/scale-ai/about

Three foundation skills for the SCALE AI skills library. Every other SCALE AI skill (hook writers, ad script writers, brief generators, etc.) reads the files these three produce before writing anything — so run these first when onboarding a new brand or client.

Note: for access to all 7 skills files, plus more AI automations & tools, check out SCALE AI: https://www.skool.com/scale-ai/about

Run them in this order:

1. **brand-dna-builder** → produces `brand/brand-dna.md`
2. **brand-voice-profiler** → produces `brand/brand-voice.md`
3. **icp-deep-dive** → produces `brand/icp-cards.md`

## What each skill does

### brand-dna-builder

Builds the brand foundation file. Scrapes the brand's website first, then asks targeted interview questions to fill the gaps the website can't answer (positioning, founder story, pillars, forbidden language, etc.). Outputs `brand/brand-dna.md` — the file every other SCALE AI skill reads before executing.

Trigger phrases: "set up brand context", "build brand DNA", "onboard a new client", "let's set up [brand name]".

### brand-voice-profiler

Builds the detailed voice rules file. Reads `brand/brand-dna.md` for context, then scrapes 2–3 real long-form copy samples from the brand's site (product pages, about page, blog) to extract actual sentence patterns. Calibrates by asking the user to rate example rewrites. Outputs `brand/brand-voice.md` with sentence structures, do/don't word lists, rhythm patterns, and voice anchors.

Trigger phrases: "build a brand voice profile", "define voice rules", "calibrate brand tone".

### icp-deep-dive

Builds 1–3 detailed ICP (ideal customer profile) cards using autonomous web research. Reads `brand/brand-dna.md`, then runs `firecrawl_agent` against the brand's category, customers, and competitors to pull real voice-of-customer language from forums, reviews, and social discussion. Optionally ingests first-party review data if the user has it. Confirms findings in a short interview, then writes `brand/icp-cards.md`.

Trigger phrases: "define my ideal customer", "build customer personas", "create ICP cards".

Requires the Firecrawl MCP for the research step. Without it, the skill falls back to interview-only mode.

## Install

These are personal Claude Code skills. Drop them into your skills directory and Claude will pick them up automatically.

```bash
git clone https://github.com/mikefutia/scale-ai-foundation-skills.git
mkdir -p ~/.claude/skills
cp -R scale-ai-foundation-skills/brand-dna-builder ~/.claude/skills/
cp -R scale-ai-foundation-skills/brand-voice-profiler ~/.claude/skills/
cp -R scale-ai-foundation-skills/icp-deep-dive ~/.claude/skills/
```

To install for a single project instead of all sessions, copy them into `.claude/skills/` inside the project root.

Verify they loaded:

```bash
ls ~/.claude/skills/
```

You should see all three folders. Start a Claude Code session and ask "build a brand DNA file" — `brand-dna-builder` should activate.

## Usage

Run from inside the project folder where you want the brand files to live (the skills write to `./brand/`).

```
> Let's set up a new brand: Acme Co, https://acme.example
```

After all three have run, your project will contain:

```
brand/
  brand-dna.md
  brand-voice.md
  icp-cards.md
```

Every downstream SCALE AI skill expects those three files at those exact paths.
