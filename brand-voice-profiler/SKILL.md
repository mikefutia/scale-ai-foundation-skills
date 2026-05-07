---
name: brand-voice-profiler
description: Builds a detailed brand voice rules file that downstream copy skills use to write in the brand's exact tone. Reads brand/brand-dna.md first for starting context, then scrapes long-form copy samples from the website (product pages, about page, blog posts) to extract specific voice patterns. Asks the user to rate example rewrites to calibrate. Saves brand/brand-voice.md with sentence structures, do/don't word lists, rhythm patterns, and voice anchors. Trigger when the user wants to build a brand voice profile, define voice rules, calibrate brand tone, or tighten how AI writes for their brand. Run this after Brand DNA Builder.
---

# Brand Voice Profiler

The second foundation skill in the SCALE AI skills library. Brand DNA Builder captures high-level voice signals (tone profile, signature language). Brand Voice Profiler goes deeper — it extracts actual sentence patterns from real brand copy, builds a do/don't word list, and calibrates voice rules that every downstream copy skill (Hook Writer, Ad Script Writer, Email Newsletter Writer, etc.) reads before writing.

## Critical Rules

- ALWAYS read `./brand/brand-dna.md` first. If it doesn't exist, tell the user to run Brand DNA Builder first — do NOT proceed without brand DNA.
- ALWAYS scrape 2-3 real copy samples from the brand's website (product pages, about page, blog, landing pages) before asking the user to rate anything.
- ALWAYS show the user at least 3 example rewrites of the same sentence in different voice directions and ask them to pick the closest match. Calibration is the whole point.
- NEVER invent voice rules that aren't grounded in real copy samples or explicit user confirmation.
- Save the final file to `./brand/brand-voice.md`.

## Process

### Step 1: Read brand DNA

Read `./brand/brand-dna.md` from the project root. If it doesn't exist, stop and tell the user:

> "I need a brand foundation file before I can build a voice profile. Run the brand-dna-builder skill first — it takes about 2 minutes and creates the file I need to read. Once you have `brand/brand-dna.md`, come back and I'll build the detailed voice rules on top of it."

Do NOT proceed without the file.

Extract the starting voice context:
- Tone profile (formal/casual, serious/playful, technical/plain)
- Voice traits
- Person/perspective
- Signature language
- Forbidden words and tones
- Brand category and ICP

This is the starting point. You're going to make it much more detailed.

### Step 2: Scrape copy samples from real brand pages

Use the same 3-tier fallback chain as Brand DNA Builder (WebFetch → Firecrawl → manual paste). Pull long-form copy from 2-3 pages where the brand actually writes in their voice:

**Priority sources:**
1. **About page or founder story** — usually the most voice-forward copy on the site
2. **A product detail page** — product descriptions reveal how the brand talks about benefits
3. **Blog post or editorial page** (if available) — long-form voice in action
4. **Email footer or newsletter signup copy** — often surprisingly voice-rich

If the brand has minimal site copy, ask the user to paste a 2-3 paragraph sample of copy that best represents the voice.

### Step 3: Extract voice patterns from the samples

Read `references/voice-dimensions.md` for the full dimension framework. Analyze the copy samples across these dimensions:

**Sentence structure:**
- Average sentence length (short/medium/long)
- Sentence variety (all similar length, or dramatic variation?)
- Fragment usage (does the brand use sentence fragments for punch?)
- Punctuation patterns (em dashes, ellipses, exclamation marks)

**Word choice:**
- Formal vs colloquial vocabulary
- Jargon level
- Adjective density
- Use of second person ("you") vs. first person ("we") vs. third person
- Contractions or no contractions

**Rhythm and pacing:**
- Staccato (short bursts) vs. flowing (longer sentences with clauses)
- Repetition patterns
- List usage in prose

**Tone modifiers:**
- Use of humor (what kind?)
- Use of directness (blunt? softened?)
- Use of authority (confident claims? hedged?)
- Use of empathy (acknowledging pain? validating?)

For each dimension, note **what the brand does** with specific quoted examples from the scraped copy.

### Step 4: Build do/don't word lists

From the copy samples and brand DNA forbidden tones:

**Do use** — 10-20 words or phrases the brand consistently uses. Pull directly from the scraped copy. These are the vocabulary anchors.

**Don't use** — 10-20 words or phrases the brand never uses or actively avoids. Combine:
- Words explicitly forbidden in brand-dna.md
- Words that clash with the brand's tone profile (e.g., "wellness journey" for Liquid Death)
- Category-generic words the brand has deliberately moved away from

### Step 5: Present voice rules to the user for confirmation

Show everything you extracted in a clean, scannable format:

```
Here's the voice profile I pulled from Magic Spoon's copy:

SENTENCE STRUCTURE
  Average length: [short/medium/long]
  Variety: [describe]
  Fragments: [used/not used]
  Example: "[quoted sentence from their copy]"

WORD CHOICE
  Formality: [level]
  Contractions: [yes/no]
  Person: [first/second/third]
  Adjective density: [describe]

RHYTHM
  Pacing: [describe]
  Example: "[quoted sentence showing rhythm]"

TONE MODIFIERS
  Humor: [type if any]
  Directness: [describe]
  Authority: [describe]

DO USE:
  [list of 10-20 words/phrases]

DON'T USE:
  [list of 10-20 words/phrases]

Does this match how you want the brand to sound? Anything to adjust?
```

Wait for user confirmation before moving on.

### Step 6: Calibrate with example rewrites

This is the most important step. Take a generic sentence and rewrite it 3-4 different ways, each in a slightly different voice direction. Ask the user which one feels most like the brand.

**Example generic sentence:** "Our cereal is made with high-quality ingredients and tastes great."

**Rewrite 1 — Direct/punchy:**
> "Real cereal. No sugar crash. Tastes like you remember, minus the guilt."

**Rewrite 2 — Playful/irreverent:**
> "Your childhood cereal grew up. It got a protein upgrade and ditched the sugar."

**Rewrite 3 — Authoritative/expert:**
> "12g of protein. 4g net carbs. The taste of the cereal aisle, engineered for adults."

**Rewrite 4 — Warm/storytelling:**
> "We made the cereal we wished existed — the one that tastes like Saturday morning without the 2pm crash."

Ask: "Which of these sounds most like the brand's voice? Or a mix of a few?"

The user's answer sharpens the voice rules. If they pick #2 with a dash of #3, you know: playful/irreverent primary, authoritative data points secondary.

Repeat this exercise with 1-2 more generic sentences if needed for precision.

### Step 7: Save the brand-voice.md file

Use the template in `references/voice-template.md`. Save to:

`./brand/brand-voice.md`

For agency projects: `./clients/[client-name]/brand/brand-voice.md`

The file should include:
- Voice summary (2-3 sentence description anyone could use as a writing prompt)
- Sentence structure rules with examples
- Word choice rules
- Rhythm and pacing rules
- Tone modifier rules
- Do-use word list with context
- Don't-use word list with rationale
- Example rewrites from the calibration step
- "How to write a headline" quick reference
- "How to write a body paragraph" quick reference

### Step 8: Confirm and suggest next steps

```
✅ Brand voice saved to ./brand/brand-voice.md

Voice summary:
"[2-3 sentence summary of how the brand sounds]"

Key do's: [5 top words/phrases]
Key don'ts: [5 top words/phrases]

Next steps in the SCALE AI system:
1. Run ICP Deep Dive to build detailed customer persona cards (the final foundation skill)
2. Then you can run any production skill (Hook Writer, Ad Script Writer, Email Newsletter Writer) and it will read both your brand DNA AND your brand voice file automatically.
```

## Required Input

- `./brand/brand-dna.md` must exist (run Brand DNA Builder first)
- Brand website URL (to scrape copy samples)
- User availability for the calibration step (picking voice rewrites)

## Output

A single file: `./brand/brand-voice.md` containing:
- Voice summary
- Sentence structure rules with real quoted examples
- Word choice rules
- Rhythm and pacing rules
- Tone modifier rules
- Do-use and don't-use word lists
- Example rewrites from calibration
- Quick reference sections for headlines and body copy

## Examples

### Example 1: Standard voice profile after brand DNA

User says: "Build the brand voice profile for Magic Spoon"

Actions:
1. Read `./brand/brand-dna.md`
2. Scrape Magic Spoon's about page and a product page via WebFetch/Firecrawl
3. Extract sentence patterns, word choice, rhythm
4. Build do/don't word lists
5. Present extraction for confirmation
6. Run calibration with 3-4 example rewrites
7. Save `./brand/brand-voice.md`
8. Suggest ICP Deep Dive next

### Example 2: Brand with minimal site copy

User says: "Build voice for a new DTC brand with a thin website"

Actions:
1. Read brand DNA (exists but thin)
2. Try to scrape — minimal copy available
3. Ask user to paste 2-3 paragraphs of sample copy that represent the voice
4. Extract patterns from the pasted samples
5. Run full calibration since automated extraction is limited
6. Save with a note that the voice is calibration-heavy

### Example 3: User wants to update an existing voice profile

User says: "We've refined our brand voice, update the voice profile"

Actions:
1. Read existing `./brand/brand-voice.md`
2. Ask what changed
3. Re-scrape if new copy is live
4. Run calibration with new example rewrites
5. Save updated file with version note

## Troubleshooting

**No brand-dna.md file exists:**
- Stop. Tell the user to run Brand DNA Builder first. Do not proceed.

**Website has minimal long-form copy:**
- Ask the user to paste 2-3 paragraphs of representative copy
- Rely heavily on the calibration step to nail the voice
- Note in the saved file that voice was calibration-heavy

**User's calibration choices contradict the brand DNA tone profile:**
- Flag the contradiction. Example: "Your brand DNA says 8/10 formal, but the calibration rewrite you picked is casual. Do you want to update the tone profile in brand-dna.md?"
- Don't silently override. Let the user reconcile.

**User picks a mix of calibration rewrites:**
- This is good. Build a hybrid voice rule. Example: "Primary tone from rewrite 2 (playful) with data specificity from rewrite 3 (authoritative)."

**Scraped copy samples are all marketing speak / generic:**
- The website might not be voice-forward. Ask the user for a better source — a founder note, an email newsletter sample, a podcast transcript.
- Never extract voice from clearly generic or boilerplate copy.
