---
name: google-ads-copy
description: Write Google Ads ad copy — Responsive Search Ads (RSAs), Performance Max asset groups, Display ads, YouTube scripts, and ad extensions. Use when the user needs headlines, descriptions, callouts, sitelinks, or any ad creative text for Google Ads. Follows Google's character limits, editorial policies, and best practices for pinning strategy.
---

# Google Ads Copy Writer

Write high-converting ad copy that complies with Google's policies, maximizes Ad Strength, and matches user intent.

## Workflow

### 1. Gather Input

Ask for if not provided:
- Product or service name
- Key differentiators / USPs (unique selling propositions)
- Target audience (who are they? what do they want?)
- Primary keyword or theme for the ad group
- Landing page URL (read it to extract language and offers)
- Tone: Professional / Friendly / Urgent / Authoritative
- Any offers, promotions, or pricing to highlight
- Competitor context (what do competitors claim?)
- Any words/phrases that MUST or MUST NOT appear

### 2. RSA (Responsive Search Ads) — Primary Format

Character limits (strict):
- Headlines: **30 characters max** each, write **15 total**
- Descriptions: **90 characters max** each, write **4 total**
- Display URL path fields: **15 characters max** each (2 fields)

#### Headline Strategy (write 15)

Distribute across these categories:

| Category | Count | Examples |
|----------|-------|---------|
| Keyword inclusion | 3 | Include the primary keyword naturally |
| Unique Value Prop | 3 | What makes them different |
| Offer / CTA | 3 | Free trial, Get a quote, Shop now |
| Social proof | 2 | "Trusted by 10,000+" / "Rated 4.8 Stars" |
| Urgency / Scarcity | 2 | "Limited Time Offer" / "Only 3 Left" |
| Feature highlights | 2 | Specific product benefits |

**Headline rules:**
- Do NOT repeat the same words across more than 3 headlines
- Do NOT use all caps except acronyms
- Do NOT use excessive punctuation or symbols
- Do NOT make claims you can't back up ("Best in the World" without proof)
- Use Title Case
- End CTAs with action verbs: Get, Start, Try, Shop, Book, Call

#### Description Strategy (write 4)

Each description should:
- Lead with the strongest benefit or offer
- Include a clear call to action
- Vary the angle across the 4 descriptions (price, feature, social proof, urgency)
- NOT repeat headlines verbatim

**Description rules:**
- End with a period or call to action — do NOT end mid-sentence
- Include the primary keyword at least once across the 4 descriptions
- One description can focus purely on offer/price if applicable

#### Pinning Recommendations

Only pin when necessary:
- Pin Headline 1: Brand name or primary keyword (if brand awareness is critical)
- Pin Headline 2: Primary offer or differentiator
- Pin Headline 3: CTA (optional)
- Never pin more than 2-3 headlines — it reduces Ad Strength and testing surface

#### Ad Strength Guide

| Ad Strength | What it means | How to fix |
|-------------|--------------|------------|
| Excellent | Google can serve optimal combos | Maintain it |
| Good | Most signals present | Add more unique headlines |
| Average | Some repetition or thin copy | Reduce duplicate words between headlines |
| Poor | Insufficient variety | Rewrite with more diverse angles |

### 3. Performance Max Asset Groups

PMax needs all asset types. Output:

**Text Assets:**
- Headlines: 15 (same rules as RSA, 30 char max)
- Long Headlines: 5 (90 char max — used in Display/YouTube)
- Descriptions: 5 (90 char max)
- Business name: [Company name]
- Call to action: Choose from: Learn More / Shop Now / Get Quote / Sign Up / Contact Us / Book Now / Subscribe / Download / Get Offer / Apply Now

**Image Asset Guidance (describe what to create/source):**
- Landscape (1.91:1) — 1200x628px min: Describe ideal image concept
- Square (1:1) — 1200x1200px min: Describe ideal image concept
- Portrait (4:5) — 960x1200px min: Describe ideal image concept
- Logo (1:1) — 1200x1200px min: Brand logo on white/transparent background
- Landscape logo (4:1) — 1200x300px min: Horizontal brand logo

**Video Asset Guidance:**
- Minimum 10 seconds, ideal 15-30 seconds for skippable
- Hook must land in first 5 seconds (before skip button appears)
- Provide a script outline if user needs one

### 4. Ad Extensions / Assets

Write all applicable assets:

#### Sitelinks (write 4-8)
- Format: `[Link Text (25 char max)] | [Description 1 (35 char)] | [Description 2 (35 char)]`
- Each sitelink should go to a distinct landing page
- Examples: Pricing, About Us, Case Studies, Free Trial, Contact

#### Callouts (write 6-10)
- 25 characters max each
- Not clickable — highlight features/benefits
- Examples: Free Shipping, 24/7 Support, No Long-Term Contracts, Money-Back Guarantee

#### Structured Snippets
Choose header type: Services, Products, Brands, Courses, Destinations, etc.
- Write 4-8 values (25 char max each)

#### Call Extension
- Include business phone if provided

#### Lead Form Extension
- Headline, description, and form fields recommendation

### 5. Policy Compliance Checks

Before finalizing, verify:
- [ ] No superlatives without proof: "Best", "#1", "World's Leading" require substantiation
- [ ] No competitor names unless running a competitor campaign (review Google's trademark policy)
- [ ] No misleading claims about pricing or availability
- [ ] No restricted content (check if category applies: healthcare, financial services, gambling, etc.)
- [ ] Dynamic keyword insertion `{KeyWord:Default}` — only use if keyword list is highly controlled
- [ ] Exclamation marks: Only 1 per ad, not in Headline 1

### 6. Output Format

```
=== RSA: [Ad Group Name] ===

HEADLINES (30 char max each):
1.  [headline] — [char count]
2.  [headline] — [char count]
...
15. [headline] — [char count]

DESCRIPTIONS (90 char max each):
1. [description] — [char count]
2. [description] — [char count]
3. [description] — [char count]
4. [description] — [char count]

DISPLAY URL: example.com / [path1] / [path2]

PINNING SUGGESTIONS:
- H1 pin: Headline #[X] — [reason]
- H2 pin: Headline #[X] — [reason]

SITELINKS:
1. [Text] | [Desc 1] | [Desc 2]
...

CALLOUTS:
[callout 1], [callout 2], [callout 3]...
```

## Key Rules
- Write for the user's intent, not for Google's algorithm — relevance wins
- Avoid writing all 15 headlines in the same voice/angle — variety = better machine learning
- Never pin so many headlines that Google can't test combinations
- Test 2 RSAs per ad group with different angles — let data decide the winner after 30 days
- Character counts are hard limits — exceeding them means the ad won't serve
