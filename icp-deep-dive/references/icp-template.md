# ICP Cards Template

Use this exact structure when saving `icp-cards.md`. Each persona gets its own card with all six dimensions filled in. Include real customer language wherever possible — never invent voice-of-customer phrases.

---

```markdown
# ICP Cards — [Brand Name]

*Generated: [YYYY-MM-DD]*
*Source: ./brand/brand-dna.md + interview + voice-of-customer data (if available)*
*Number of personas: [1-3]*

---

## Persona 1: [Memorable name — e.g., "Burned-Out Brad" or "Skeptical Sarah"]

*One-line summary: [10-15 word description that captures the persona instantly]*

### Identity

- **Age:** [range]
- **Role/life stage:** [job, life stage, e.g., "Mid-career marketing manager, recently promoted, no kids"]
- **Family situation:** [single, partnered, kids, etc.]
- **Geographic context:** [urban/suburban/rural, region if relevant]

### Lifestyle and Values

- **How they spend their time:** [2-3 sentence summary of a typical week]
- **What they value:** [3-5 specific things — health, status, family, freedom, etc.]
- **What they want more of:** [time, energy, confidence, recognition, etc.]
- **What they're trying to escape:** [burnout, boredom, financial stress, feeling out of shape, etc.]

### The Specific Pain

- **The exact problem:** [Specific. Not "they want to feel better." What's actually broken?]
- **How long they've had it:** [duration — weeks, months, years]
- **What they've tried:** [list of failed attempts — competitor products, free alternatives, lifestyle changes]
- **What it's costing them:** [time, money, energy, relationships, opportunities]
- **The emotional cost:** [how it makes them feel — frustrated, resigned, embarrassed, overwhelmed]

### Buying Triggers

- **The "I need this NOW" moment:** [Specific scenario. What just happened that pushed them over the edge?]
- **Internal narrative:** [their self-talk — "I deserve this," "I can't keep doing this," etc.]
- **External trigger:** [event, deadline, season, social pressure]
- **Budget psychology:** [price-sensitive / value-driven / premium-comfortable]

### Objections and Hesitations

- **Top hesitations:**
  1. [Reason 1]
  2. [Reason 2]
  3. [Reason 3]
- **What they're skeptical about:** [category-wide trust issues, claims that sound too good to be true]
- **What needs to be proven:** [evidence required — reviews, clinical data, founder story, guarantee, free trial]
- **Competitors they're comparing:** [direct competitors, indirect alternatives, "do nothing"]

### Language and Media

- **Voice-of-customer phrases:**
  - "[Exact phrase 1]"
  - "[Exact phrase 2]"
  - "[Exact phrase 3]"
  - "[Exact phrase 4]"
  - "[Exact phrase 5]"
- **Platforms they spend time on:** [Instagram, TikTok, Reddit, YouTube, podcasts, etc.]
- **Who they follow:** [specific creators, influencers, accounts]
- **What they read/watch/listen to:** [publications, shows, podcasts, newsletters]
- **Marketing they respond to:** [examples of ads/brands that have worked on them]

---

## Persona 2: [Name] (if applicable)

*[Same structure as Persona 1 — all six dimensions]*

---

## Persona 3: [Name] (if applicable)

*[Same structure as Persona 1 — all six dimensions]*

---

## How to Use These Cards

Every SCALE AI production skill that targets specific personas will read this file and reference the relevant card. Examples:

- **Hook Writer (Meta Ads)** — generates separate hook batches per persona
- **Ad Script Writer** — writes scripts that open with persona-specific pain
- **Email Sequence Writers** — segments email flows by persona
- **Landing Page Copy Writer** — writes pages that lead with the dominant persona's language
- **Creative Brief Generator** — builds briefs that specify which persona the creative is targeting

If you have multiple personas, you can ask production skills to focus on a specific one:

> "Use hook-writer-meta to generate 20 hooks for Magic Spoon, focused on Persona 1 (Burned-Out Brad)."

The skill will read this file, find Persona 1, and calibrate the hooks to that specific customer.

---

## Metadata

- **ICP cards version:** 1.0
- **Last updated:** [YYYY-MM-DD]
- **Source data:** [research-driven (Firecrawl Agent) / first-party + research / interview-only]

## Research Sources

*If the cards were built with Firecrawl Agent, list the URLs the agent pulled from. This is for verification and lets the user check the original sources.*

- [URL 1] — [brief description of what was found]
- [URL 2] — [brief description]
- [URL 3] — [brief description]
- (Continue for all sources Firecrawl Agent returned)

*If interview-only, omit this section or note "No web research performed."*
```

---

## Template Rules

1. **Every dimension must be filled in for every persona.** Incomplete cards produce weaker downstream output.
2. **Voice-of-customer phrases must be real.** Pull from reviews, surveys, support tickets, or direct user input. Never invent customer language.
3. **Persona names matter.** Use memorable labels ("Burned-Out Brad," "Skeptical Sarah") so downstream skills can reference them by name.
4. **One-line summaries at the top of each card.** These get scanned by other skills as quick context — make them sharp.
5. **Maximum 3 personas per file.** If a brand has more, run the skill multiple times with different focus areas and save additional files (`icp-cards-v2.md`, etc.).
6. **The "How to Use These Cards" section is required.** It tells the user how to invoke specific personas in downstream skills.
