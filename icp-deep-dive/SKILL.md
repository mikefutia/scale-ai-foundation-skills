---
name: icp-deep-dive
description: Builds detailed ideal customer profile (ICP) cards using autonomous web research via Firecrawl Agent. Reads brand/brand-dna.md first, then runs deep research on the brand's category, customers, and competitors to extract real customer language, pain points, and behavior patterns. Optionally pulls voice-of-customer data from user-provided reviews. Confirms findings with a short interview, then saves brand/icp-cards.md. Trigger when the user wants to define their ideal customer, build customer personas, create ICP cards, or set up persona-specific targeting for ads and content. Run this after Brand DNA Builder and Brand Voice Profiler.
---

# ICP Deep Dive

The third foundation skill in the SCALE AI skills library. Most ICP exercises rely on the brand owner guessing what their customer looks like. ICP Deep Dive doesn't guess — it uses Firecrawl Agent to autonomously research the brand's category, customers, and competitors on the web, pulling real voice-of-customer language and behavior patterns from forums, reviews, and social discussion. Then it confirms with a short interview before saving 1-3 detailed persona cards that downstream production skills read.

## Critical Rules

- ALWAYS read `./brand/brand-dna.md` first. If it doesn't exist, tell the user to run Brand DNA Builder first.
- ALWAYS try `firecrawl_agent` for research first. If Firecrawl MCP isn't installed, gracefully fall back to interview-only mode and explain the tradeoff.
- ALWAYS ask the user upfront whether they have customer reviews, surveys, or other research data to share. Real first-party data beats web research when available.
- ALWAYS use real customer language wherever possible — quote directly from research findings, never invent voice-of-customer phrases.
- NEVER build more than 3 personas in a single run. If the user wants more, run the skill multiple times.
- Save the final file to `./brand/icp-cards.md`.

## Process

### Step 1: Foundation file check

Check for the foundation files:

1. `./brand/brand-dna.md` (REQUIRED)
2. `./brand/brand-voice.md` (recommended)

For agency project structures, check `./clients/[client-name]/brand/` instead.

**If `brand-dna.md` is missing:**
> "I need a brand foundation file before I can build ICP cards. Run the brand-dna-builder skill first."

**If `brand-dna.md` exists but `brand-voice.md` is missing:**
> "I found your brand DNA. I can build ICP cards now, but I'd recommend running brand-voice-profiler too — it'll make every downstream production skill much sharper. Want me to proceed, or run Brand Voice Profiler first?"

### Step 2: Extract starting context from brand DNA

From `brand-dna.md`, pull:
- **Category** (e.g., supplements, skincare, apparel) — drives the research scope
- **Target customer summary** — the high-level starting point
- **Core problem solved** — the central pain
- **Top competitors** — these become research targets
- **Priority products** — what to focus the research on

This becomes the input to the research phase.

### Step 3: Ask about existing customer data

Before running automated research, ask the user:

> "Before I research your customers on the web, do you have any of these you can share?
>
> 1. **Customer reviews** — Trustpilot, Amazon, Google, Shopify, etc.
> 2. **Survey responses** — recent customer surveys or NPS feedback
> 3. **Support tickets or chat logs** — common questions, complaints, themes
> 4. **Social comments or DMs** — what customers say in your inbox or comments
> 5. **None of the above — go straight to web research**
>
> First-party data is more accurate than what I can find on the web. If you have any, paste it now and I'll use it as the foundation."

If the user has data, parse it for:
- Recurring pain points
- Common questions
- Direct quotes that capture customer language
- Demographic or lifestyle signals
- Objections and hesitations

This becomes the highest-priority data source for the persona cards.

### Step 4: Run autonomous web research with Firecrawl Agent

Use the `firecrawl_agent` tool from the Firecrawl MCP server to run autonomous research. Build a research prompt tailored to the brand.

**Research prompt template:**

```
Research the ideal customer profile for [BRAND NAME], a [CATEGORY] brand that sells [PRIORITY PRODUCT] and helps customers with [CORE PROBLEM]. Their main competitors are [COMPETITOR LIST].

Focus your research on:

1. **Who is buying products in this category?** Demographics, life stage, lifestyle. Look at Reddit discussions, customer reviews on competitor sites, and forum threads.

2. **What specific problems or pain points are they trying to solve?** Find the actual language customers use. Pull direct quotes when possible.

3. **What have they already tried that didn't work?** What competing products, DIY solutions, or lifestyle changes have they attempted before considering this category?

4. **What are the most common objections and hesitations?** Why do people NOT buy in this category? What are they skeptical about?

5. **Where do these customers spend time online?** Which subreddits, communities, hashtags, or platforms are they active in?

6. **What language do they use to describe their problem?** Pull at least 5-10 exact phrases from real customer discussions, reviews, or comments.

7. **What's the typical buying trigger?** What event or moment makes someone in this category decide they're finally ready to buy?

Return findings as structured insights with source URLs for verification.
```

Pass this prompt to `firecrawl_agent` with these arguments:

```json
{
  "prompt": "[the research prompt above]",
  "schema": {
    "type": "object",
    "properties": {
      "demographics": { "type": "string" },
      "pain_points": { "type": "array", "items": { "type": "string" } },
      "failed_solutions": { "type": "array", "items": { "type": "string" } },
      "objections": { "type": "array", "items": { "type": "string" } },
      "platforms": { "type": "array", "items": { "type": "string" } },
      "voice_of_customer_quotes": { "type": "array", "items": { "type": "string" } },
      "buying_triggers": { "type": "array", "items": { "type": "string" } }
    }
  }
}
```

The agent runs asynchronously. Tell the user:

> "I'm running autonomous research on your customers right now. This usually takes 2-5 minutes — Firecrawl Agent is browsing the web, reading discussions, and pulling real customer language. I'll let you know when it's done."

Poll `firecrawl_agent_status` every 30 seconds until the job completes (or 5 minutes pass, whichever comes first).

**If `firecrawl_agent` is not available** (Firecrawl MCP not installed):
> "I can't run autonomous web research because the Firecrawl MCP server isn't installed in your Cowork. I'll proceed with interview-only mode, which works but produces less detailed personas. To install Firecrawl, [link to Firecrawl setup video]. Continuing with interview..."

Then skip to Step 6 and run the interview-only flow.

### Step 5: Synthesize research findings

Once `firecrawl_agent` completes:

1. Extract the structured data it returned
2. Combine with any user-provided customer data from Step 3
3. Determine how many distinct personas the data suggests:
   - One dominant persona pattern → 1 card
   - Two clearly different segments → 2 cards
   - Three distinct patterns → 3 cards (cap)

Present a research summary to the user:

```
Here's what I found from researching [brand category] customers:

PATTERNS DETECTED
- [Demographic pattern 1]
- [Demographic pattern 2]
- [Behavior pattern]

KEY PAIN POINTS (from real discussions)
- "[Real quote 1]"
- "[Real quote 2]"
- "[Real quote 3]"

COMMON FAILED SOLUTIONS
- [What they tried that didn't work]

TOP OBJECTIONS
- [Objection 1]
- [Objection 2]

PLATFORMS WHERE THEY HANG OUT
- [Platform list with context]

Based on this research, I see [1/2/3] distinct customer segment(s) for [brand]. Want me to build [1/2/3] persona cards, or adjust the count?
```

Wait for user confirmation on persona count.

### Step 6: Run a short refinement interview

For each persona, ask only the questions the research couldn't answer or where you need user confirmation. Read `references/icp-questions.md` for the full question set.

Skip questions where the research already gave you a confident answer. Focus on:

- **Confirming demographics** — the user knows their actual customer base better than research can guess
- **Buying triggers** — what specific event or moment pushes their customers to buy
- **Budget psychology** — price-sensitive vs. premium-comfortable
- **Persona naming** — give each persona a memorable label ("Burned-Out Brad," "Skeptical Sarah") the user picks or confirms

The interview should be FAST. Three to six questions max per persona. Cowork's wizard UI handles pacing.

### Step 7: Build and present the persona cards

For each persona, combine:
1. Research findings from Firecrawl Agent
2. User-provided customer data from Step 3
3. Refinement answers from Step 6

Build a complete persona card following the structure in `references/icp-template.md`. The card should have all six dimensions:

- Identity
- Lifestyle and Values
- The Specific Pain
- Buying Triggers
- Objections and Hesitations
- Language and Media

Present the card to the user for confirmation:

```
PERSONA 1: [Name]

[Display all six dimensions with research-backed details and quoted customer language]

This card is built from:
- Web research (Firecrawl Agent)
- Your customer data (if provided)
- Your refinement answers

Anything to adjust before I save?
```

Let the user correct anything that feels off. Repeat for each persona.

### Step 8: Save the icp-cards.md file

Use the template in `references/icp-template.md`. Save to:

`./brand/icp-cards.md`

For agency projects: `./clients/[client-name]/brand/icp-cards.md`

The file should contain:
- 1-3 persona cards
- A "Sources" section listing the URLs Firecrawl Agent pulled from (for verification)
- A note on which sections were research-derived vs. user-confirmed vs. interview-only

### Step 9: Confirm and suggest next steps

```
✅ ICP cards saved to ./brand/icp-cards.md

[X] persona cards created:
1. [Persona name 1] — [one-line summary]
2. [Persona name 2] — [one-line summary] (if applicable)
3. [Persona name 3] — [one-line summary] (if applicable)

Research summary:
- Sources analyzed: [count from Firecrawl Agent]
- Customer quotes pulled: [count]
- First-party data used: [yes/no]

You now have all three foundation files complete:
✅ brand-dna.md
✅ brand-voice.md
✅ icp-cards.md

You're ready to run any production skill in the SCALE AI library. Every production skill will read all three foundation files and produce output calibrated to your brand, voice, and customers.
```

## Required Input

- `./brand/brand-dna.md` must exist
- Firecrawl MCP installed (for the research-first flow — falls back to interview-only if not)
- Optional: customer reviews, survey data, support tickets, social comments

## Output

A single file: `./brand/icp-cards.md` containing 1-3 detailed persona cards, each with six dimensions backed by real research and verified customer language. Includes a Sources section for verification.

## Examples

### Example 1: Standard research-driven setup

User says: "Build the ICP cards for Magic Spoon"

Actions:
1. Read `./brand/brand-dna.md`
2. Ask about existing customer data — user has none
3. Run `firecrawl_agent` to research high-protein cereal customers, competitor reviews (Catalina Crunch, Three Wishes), Reddit discussions in r/keto, r/intermittentfasting
4. Wait for the agent to complete (2-5 minutes)
5. Synthesize findings — identify one dominant persona pattern
6. Show research summary, confirm 1 persona
7. Run a short 5-question refinement interview
8. Build the persona card with research-backed quotes and patterns
9. Save to `./brand/icp-cards.md`

### Example 2: User has customer reviews

User says: "Build ICP cards. I have a CSV of 200 Trustpilot reviews."

Actions:
1. Read brand DNA
2. Ask user to paste a representative sample of the reviews
3. Extract pain points, language, and themes from the reviews
4. ALSO run `firecrawl_agent` for additional research on the broader category
5. Combine first-party review data with web research
6. Build persona cards with first-party quotes prioritized over web quotes
7. Save with a note that the cards are review-data-enriched

### Example 3: Firecrawl not installed (fallback)

User says: "Build ICP cards for Magic Spoon"

Actions:
1. Read brand DNA
2. Try `firecrawl_agent` — tool not found
3. Tell user: "Firecrawl MCP isn't installed. I'll use interview-only mode, which is less detailed. Want to install Firecrawl first or proceed with interview only?"
4. If user proceeds, run the full interview from `references/icp-questions.md`
5. Build persona cards based on user answers alone
6. Save with a note that cards are interview-only (no web research)

## Troubleshooting

**Firecrawl Agent times out or returns minimal data:**
- The brand category might be too niche or have minimal public discussion. Fall back to a longer user interview.
- Try a more specific research prompt focused on competitors instead of the brand directly.

**Research findings contradict the user's intuition about their customers:**
- This is valuable information, not a problem. Surface the contradiction explicitly: "Research suggests [X], but you mentioned [Y] — which feels more accurate to you?"
- The user usually knows their actual customers better than web research can guess, but sometimes the research surfaces blind spots.

**User pastes too much customer data to process:**
- Ask for a sample (10-20 reviews, not 500). Tell them you'll extract patterns from the sample.
- Suggest they prioritize 3-star reviews — those reveal more about objections than 5-star reviews.

**Multiple personas look very similar after research:**
- Push back. Ask: "Are these really distinct customer segments, or different stages of the same customer journey? If they're the same person at different times, build one persona with multiple buying triggers instead of multiple personas."

**User wants to skip research and go straight to interview:**
- Honor the request but flag the tradeoff: "Research-driven personas are usually more accurate because they pull real customer language. Interview-only mode produces personas based on your assumptions. Want to proceed with interview only?"
