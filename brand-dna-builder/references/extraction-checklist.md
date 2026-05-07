# Website Extraction Checklist

Use this checklist when scraping a brand's website. Extract every applicable item. If something isn't present on the page, leave it blank — do not guess.

## Visual Identity

### Colors
Extract every prominent color and report the exact hex value:
- **Primary color**: most prominent brand color, usually on CTAs, headers, and logo
- **Secondary color**: supporting color used on subheadings, accents
- **Accent color**: highlight or callout color used on badges, promotional elements
- **Background**: main page background
- **Text**: primary body text color
- **Link color**: if different from primary

Look in CSS, inline styles, and rendered elements. Report colors as: `name` `#hex` — usage context.

### Typography
Read the actual `font-family` declarations in CSS, `<link>` tags (Google Fonts / Typekit / custom font URLs), and inline styles. Report the exact font names used for:
- Headings (H1, H2)
- Body text
- Buttons/CTAs
- Any notable accent fonts (display, script, etc.)

Do NOT report generic fallbacks like "sans-serif" or "serif." Extract the actual named font.

### Logo
- Text-based, icon-based, or combined?
- Logo color and placement
- Any tagline next to the logo?

### Visual Style
Describe what you observe in 1-2 sentences:
- Minimal with whitespace? Bold and saturated? Dark mode? Gradient-heavy?
- Illustration-driven? Photography-driven? Corporate? Editorial?
- Spacing: tight and information-dense, or airy and spacious?

### Photography Style
- Product photography: flat/lifestyle/editorial/minimal/studio?
- Model photography: diverse/curated/aspirational/UGC-style?
- Color treatment: warm/cool/natural/filtered?
- Background treatment: plain/contextual/branded?

### Button Style
- Shape: pill, rounded, square, sharp corners?
- Color: filled or outlined?
- Text color on buttons
- Hover behavior if visible

## Copy & Messaging

### Hero Section
- Exact H1 or hero headline (word-for-word)
- Hero subheading if present
- Hero CTA button text
- Any hero image or video description

### Tagline
- Brand tagline or slogan if shown in header, footer, or hero

### Value Proposition
- The main "what we do and why it matters" statement
- Usually in the hero section or right after

### Key Benefits
Extract 3-5 main benefits from the homepage. Look for:
- Benefit-led section headings
- Feature/benefit callout blocks
- Icons with short descriptions
- "Why choose us" sections

### CTAs
Every call-to-action button on the page. Report the exact text.

### Navigation
Main nav items — these reveal product categories, page structure, and priority pages.

### Social Proof
- Testimonials: how many? Include 1-2 exact quotes if present.
- Customer logos: any "as seen in" or press logos?
- Ratings/reviews: stars displayed? Review count?
- Metrics: "10,000+ customers" type claims
- Trust badges: security, guarantees, certifications
- Awards: any industry recognition shown?

## Brand Voice Signals

Read the site copy and assess:

### Tone
- Formal vs casual (1-10 scale)
- Serious vs playful (1-10 scale)
- Technical vs plain language (1-10 scale)
- Professional vs conversational (1-10 scale)

### Person/Voice
- First person ("we help", "our mission")
- Second person ("you can", "your results")
- Third person ("customers love", "the [product]")

### Notable Language
- Any repeated brand-specific words or phrases
- Trademarked terms or proprietary concepts
- Unique product naming conventions

### Writing Style
- Sentence length (short punchy vs. flowing)
- Use of lists vs prose
- Emoji usage in copy
- Exclamation mark frequency

## Business Model Signals

Look for indicators of:
- **DTC**: Shop Now buttons, shopping cart, product pages, checkout
- **Subscription**: "subscribe and save", recurring pricing, subscription boxes
- **Marketplace**: multiple brands/sellers, third-party products
- **Service**: consultation requests, demo bookings, pricing pages

## Category Detection

Identify the product category based on:
- Navigation labels
- Product names and descriptions
- Imagery
- Industry-specific terminology

Common DTC categories: skincare, supplements, apparel, food/beverage, home goods, pet, beauty, fitness, wellness, accessories.

## What NOT to Extract

Do not include:
- Blog post content (unless directly about the brand)
- Generic footer links (privacy, terms, shipping)
- Newsletter signup forms (unless they reveal positioning)
- Third-party widget content (chat bots, review widgets)
