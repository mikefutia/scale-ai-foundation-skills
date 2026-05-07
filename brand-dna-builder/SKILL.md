---
name: brand-dna-builder
description: Builds a comprehensive Brand DNA file by scraping the brand's website first, then filling gaps with targeted interview questions. Trigger on any request to set up brand context, build a brand foundation, create a brand DNA file, or onboard a new brand/client into the SCALE AI skills system. Also trigger when the user mentions setting up a new project, adding a new client, or any phrase like "let's set up [brand name]". This skill creates the foundational brand/brand-dna.md file that every other SCALE AI skill reads before executing.
---

# Brand DNA Builder

The foundation skill for the SCALE AI skills library. Builds a comprehensive `brand/brand-dna.md` file by scraping the brand's website and filling gaps through targeted interview questions. Every other SCALE AI skill reads this file before executing, so accuracy matters — don't guess, don't fill in defaults.

## Critical Rules

- NEVER guess or invent brand details. Extract from the live website or ask the user directly.
- ALWAYS scrape the website first before asking interview questions. Only ask about things the website cannot tell you.
- ALWAYS save the final file to `./brand/brand-dna.md`. Create the `brand/` folder if it doesn't exist.
- ALWAYS confirm the extracted data with the user before saving.
- If the user is an agency managing multiple clients, save to `./clients/[client-name]/brand/brand-dna.md` instead.

## Process

### Step 1: Ask for the brand name and URL

Start with a single question:

> "Let's build your Brand DNA. What's the brand name and website URL?"

If the user is an agency and says they're setting up a client, ask for the client name too and use the agency folder structure (`./clients/[client-name]/brand/`).

### Step 2: Scrape the homepage (3-tier fallback)

Read `references/extraction-checklist.md` first so you know exactly what to pull.

Try the following methods in order. Stop at the first one that works:

**Tier 1 — WebFetch (try first):**
Use the built-in WebFetch tool on the homepage URL. This is the fastest and free path. Many DTC brand sites work fine with it.

**Tier 2 — Firecrawl MCP (if WebFetch is blocked):**
If WebFetch returns an error like "Access blocked," "Cloudflare," or returns empty/malformed content, try the `firecrawl_scrape` tool from the Firecrawl MCP server. This handles Cloudflare protection, JavaScript rendering, and aggressive bot blocking that defeats WebFetch.

Use these arguments:
```json
{
  "url": "[homepage URL]",
  "formats": ["markdown"],
  "onlyMainContent": true
}
```

If the user doesn't have Firecrawl MCP installed, you'll get a "tool not found" error. In that case, gracefully tell them:

> "I couldn't fetch the site automatically — your default WebFetch is blocked on this domain (common with DTC sites using Cloudflare). The smoothest fix is installing the Firecrawl MCP connector in Cowork settings (about 3 minutes — sign up at firecrawl.dev for a free API key, then add the connector URL). Or, if you prefer, you can paste the homepage content directly into this chat and I'll extract from that. Which would you like?"

**Tier 3 — Manual paste (zero-setup fallback):**
If the user opts for manual paste or both auto-methods fail, ask them to paste the homepage content as text. Then extract from the pasted content using the same checklist. Note in the saved file that extraction was done from manual paste.

Do NOT guess or assume. If a color, font, or value prop isn't visible in the source, leave it blank — you'll ask the user in Step 5.

### Step 3: Scrape additional pages if needed

If the homepage leaves significant gaps, also fetch:
- `/about` or `/about-us` — company story, mission, team, voice signals
- `/products` or shop page — product categorization, positioning
- A product detail page — product copy voice, benefit framing, social proof

Use the same 3-tier fallback chain from Step 2. Only fetch additional pages if they'll genuinely fill gaps. Don't fetch for the sake of it.

### Step 4: Present the extraction to the user

Show everything you extracted in a clean, scannable format. Use this structure:

```
Here's what I pulled from [website]:

BRAND
  Name: [name]
  Tagline: "[extracted tagline]"
  Category: [detected category — e.g., skincare, supplements, apparel]
  Business model: [DTC / marketplace / subscription / hybrid]

VISUAL IDENTITY
  Primary color:    [name] #[hex] — used on [CTAs, headers]
  Secondary color:  [name] #[hex] — used on [subheads, accents]
  Accent color:     [name] #[hex] — used on [highlights, badges]
  Background:       #[hex]
  Text:             #[hex]

  Heading font: [exact font name]
  Body font:    [exact font name]

  Visual style: [1-2 sentence description of what you observed]
  Photography:  [product photography style — minimal/lifestyle/editorial/etc.]
  Button style: [pill/rounded/square, color, hover behavior if visible]

COPY & MESSAGING
  Hero headline: "[exact H1 or hero text]"
  Value prop:    "[extracted value proposition]"
  Key benefits:  [3-5 benefits from the homepage]
  CTAs found:    "[CTA 1]", "[CTA 2]", "[CTA 3]"

SOCIAL PROOF
  Testimonials: [yes/no, how many, who]
  Reviews/ratings: [shown? where? how many?]
  Press/awards: [any logos or mentions]
  Customer count: [if displayed]

BRAND VOICE SIGNALS
  Tone: [formal/casual], [serious/playful], [technical/plain]
  Person: [first person "we" / second person "you" / third person]
  Notable language: [any repeated brand-specific words or phrases]

Does this look right? Anything to correct or add?
```

Wait for the user to confirm or correct. Do NOT proceed until they've reviewed the extraction.

### Step 5: Fill gaps with interview questions

After the user confirms the extraction, ask about things the website cannot tell you. Read `references/interview-questions.md` for the full question set.

Only ask about:
- **Target customer specifics** — the website rarely reveals ICP details beyond the obvious
- **Brand voice intent** — what the brand *wants* to sound like, which may differ from current copy
- **Positioning and differentiators** — why customers choose this brand over alternatives
- **What's forbidden** — words, claims, or tones the brand avoids
- **Priority products or SKUs** — which products matter most for ads and content
- **Competitive context** — who they compete with and how they position against them

Do NOT re-ask about anything the website already answered (colors, fonts, tagline, visual style, value prop).

Ask questions in batches of 3-4 at a time. Don't dump 20 questions at once.

### Step 6: Write the brand-dna.md file

Use the canonical format in `references/brand-dna-template.md`. Fill in every section using only:
1. Data extracted from the website (Step 2-3)
2. User answers from the interview (Step 5)

If a field has no data, leave it blank or omit the section. **Never fill in placeholders or defaults.**

Save to `./brand/brand-dna.md` (or `./clients/[client-name]/brand/brand-dna.md` for agencies).

### Step 7: Confirm and suggest next steps

```
✅ Brand DNA saved to ./brand/brand-dna.md

Summary:
  Brand: [name]
  Category: [category]
  Colors: [primary] [secondary] [accent]
  Voice: [tone summary]
  Audience: [ICP summary]

Next steps in the SCALE AI system:
1. Run Brand Voice Profiler to define tone and voice rules in detail
2. Run ICP Deep Dive to build customer persona cards
3. Then you can run any production skill (Hook Writer, Creative Brief Generator, etc.) and it will read this file automatically.

Want to continue with Brand Voice Profiler now?
```

## Required Input

- Brand name
- Brand website URL
- (Optional) Client name, if agency setup

Everything else is extracted or collected through the process.

## Output

A single file: `./brand/brand-dna.md` (or `./clients/[client-name]/brand/brand-dna.md`)

The file follows the template in `references/brand-dna-template.md` and contains:
- Brand identity (name, tagline, category, business model)
- Visual identity (colors, fonts, photography style, button style)
- Copy and messaging (hero, value prop, benefits, CTAs)
- Social proof available
- Brand voice signals (tone, person, notable language)
- Target customer summary (from interview)
- Positioning and differentiators (from interview)
- Forbidden words or tones (from interview)
- Priority products (from interview)
- Competitive context (from interview)

## Examples

### Example 1: Standard DTC brand setup

User says: "Let's set up brand DNA for Kitsch — kitsch.com"

Actions:
1. WebFetch kitsch.com homepage
2. Extract colors, fonts, copy, visual style, value props
3. Present extraction to user for confirmation
4. Ask interview questions about target customer, positioning, forbidden tones
5. Write to `./brand/brand-dna.md`
6. Confirm and suggest Brand Voice Profiler next

### Example 2: Agency setting up a new client

User says: "I'm onboarding a new client — their brand is Maelys, maelys.com"

Actions:
1. Ask if this is a new agency client (it is)
2. Use folder path `./clients/maelys/brand/brand-dna.md`
3. WebFetch maelys.com homepage
4. Same extraction + interview flow
5. Save to the client-specific path
6. Suggest Brand Voice Profiler with the same client folder

### Example 3: Brand with minimal website content

User says: "Set up brand DNA for a new Shopify store — the URL is [minimal-site.com]"

Actions:
1. WebFetch the homepage
2. Notice the extraction yielded minimal copy and voice signals
3. Also fetch the /about and a product page to gather more
4. Present combined extraction to user
5. Rely more heavily on the interview to fill gaps
6. Save with a note in the file that extraction was limited

## Troubleshooting

**WebFetch returns "blocked," "Cloudflare," or empty content:**
- This is common with DTC sites. Fall back to `firecrawl_scrape` from the Firecrawl MCP server.
- If Firecrawl isn't installed, offer manual paste as the third fallback.

**Firecrawl tool not found:**
- The user hasn't installed the Firecrawl MCP connector. Offer two paths:
  1. Install Firecrawl: sign up at firecrawl.dev (free tier), grab the API key, add the connector URL `https://mcp.firecrawl.dev/{api-key}/v2/mcp` in Cowork settings
  2. Manual paste: ask them to copy the homepage content into the chat

**WebFetch returns minimal or malformed content:**
- Try fetching /about or a product page for additional context
- If still minimal, fall back to Firecrawl or manual paste
- Note in the saved file that extraction was limited

**User corrects most of the extracted data:**
- Don't argue. Update everything per user corrections before saving.
- This sometimes happens when a brand is mid-rebrand or has outdated web copy.

**Multiple conflicting color schemes on the site:**
- Ask the user which is the current/primary brand palette
- Don't try to guess from frequency alone

**User skips interview questions:**
- Save what you have. A partial brand DNA is still useful.
- Mention which sections are incomplete so they can add context later.

**Agency user wants to migrate existing brand context:**
- Ask if they have an existing brand guide or voice document
- If yes, offer to extract structured data from it and combine with website scrape
