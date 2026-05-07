# Voice Dimensions Reference

Use this framework when analyzing scraped brand copy. For each dimension, identify what the brand does and quote real examples from the copy samples.

## 1. Sentence Structure

### Length
- **Short** (under 10 words): punchy, staccato, high-impact
- **Medium** (10-20 words): balanced, conversational
- **Long** (20+ words): flowing, editorial, sophisticated

Most brands use a mix. Note which length dominates and which is used for emphasis.

### Variety
- **Uniform**: all sentences similar length — rhythmic but can feel monotonous
- **Varied**: dramatic swings between short and long — creates punch and pace
- **Rhythmic**: patterned variety (e.g., long-short-short, long-short-short)

### Fragments
Does the brand use sentence fragments as punctuation? Example: "Real cereal. No sugar. Finally." vs. "Our cereal is real and has no sugar."

### Punctuation patterns
- **Em dashes**: signals a conversational, interrupted flow
- **Ellipses**: signals a thoughtful pause or tease
- **Exclamation marks**: frequency and tone (excited vs. aggressive vs. none at all)
- **Parenthetical asides**: signals a casual, chatty voice
- **Colons for callouts**: signals a structured, list-friendly voice

## 2. Word Choice

### Formality
1-10 scale. Note specific words that anchor the level:
- 1-3: street/slang (e.g., "lit", "no cap", "fire")
- 4-6: casual professional (e.g., "great", "really good", "solid")
- 7-10: formal/technical (e.g., "exceptional", "rigorous", "clinically-demonstrated")

### Jargon
- **None**: completely plain language
- **Light**: occasional technical terms explained in context
- **Heavy**: assumes audience knows the terminology
- **Brand-specific**: invents its own language (e.g., Apple's "Pro motion", Peloton's "Power Zones")

### Contractions
Does the brand use "don't/can't/won't" or "do not/cannot/will not"? This is a big formality indicator.

### Adjective density
- **Sparse**: nouns and verbs do most of the work
- **Moderate**: adjectives used for key benefits
- **Dense**: lots of modifiers stacked (e.g., "premium, clinically-proven, dermatologist-approved")

### Person/Perspective
- **First person plural ("we")**: brand speaks as a team or company
- **Second person ("you/your")**: directly addresses the customer
- **Third person**: talks about the product or customer objectively
- **Switching**: uses multiple — note the pattern (e.g., "we" for mission, "you" for benefits)

## 3. Rhythm and Pacing

### Pacing
- **Staccato**: short bursts, high energy, scroll-stopping
- **Flowing**: longer sentences with subordinate clauses, editorial
- **Mixed**: deliberate rhythm shifts for emphasis

### Repetition patterns
Does the brand use anaphora (repeated sentence openings)? Example:
> "Better for your body. Better for your morning. Better than you remember."

Repetition is a high-impact voice signal. Note if the brand uses it.

### List usage in prose
- Uses bulleted lists heavily vs. flowing prose only
- Lists inside sentences ("We use real ingredients, real science, and real results")
- Triads (lists of three) — a classic rhythm pattern

## 4. Tone Modifiers

### Humor
- **None**: earnest brand
- **Subtle wit**: occasional clever phrasing, not jokes
- **Playful**: frequent light humor
- **Irreverent**: challenging, provocative, rule-breaking
- **Absurdist**: surreal, over-the-top (rare — think Liquid Death)

Note the specific type and quote an example.

### Directness
- **Blunt**: says exactly what it means, no softening
- **Direct**: clear but polite
- **Soft**: hedged, qualified, careful
- **Hedged**: uses "maybe", "might", "can help"

### Authority
- **Confident claims**: makes strong statements without hedging
- **Balanced**: mixes confident claims with honest caveats
- **Humble**: under-promises, lets results speak
- **Hedged**: everything qualified

### Empathy
- **Acknowledged**: directly names customer pain or frustration
- **Implied**: assumes the reader relates without explicitly stating
- **Absent**: product-focused, doesn't reference emotional state

## 5. Voice Anchors

After analyzing all dimensions, try to capture the brand's voice in 3-5 anchor adjectives that a writer could use as a prompt. Examples:

- Liquid Death: **chaotic, irreverent, absurdist, direct**
- Apple: **confident, precise, aspirational, minimal**
- Glossier: **warm, intimate, conversational, effortless**
- Magic Spoon: **playful, confident, nostalgic, data-led**

These anchors become the "write like this" prompt every downstream copy skill uses.

## 6. What to Quote in the Output

For every dimension, include at least one direct quote from the scraped copy. Real examples are more useful than abstract rules. A copy skill reading the voice file should be able to see the pattern in action, not just hear a description of it.

Example of a good voice rule in the output:

> **Sentence structure:** Short, punchy sentences dominate, with longer explanatory sentences used for data points or product detail.
>
> Quoted example (homepage hero):
> > "Not your childhood cereal. Same taste. Zero sugar. 12g of protein per bowl."

Example of a bad voice rule:

> **Sentence structure:** The brand uses a variety of sentence lengths to create rhythm.

The first one is usable. The second one is vague and downstream skills can't act on it.
