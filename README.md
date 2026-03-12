# Schema Markup Skill for Claude

An AI agent skill that generates accurate, complete Schema.org JSON-LD markup — optimized for both Google Rich Results and AI answer engines (ChatGPT, Perplexity, Google AI Overviews, Claude).

## What makes this different

Most schema tools generate basic markup for Google. This skill also covers **AEO (Answer Engine Optimization)** — helping AI systems understand your brand, cite your content, and surface your products in AI-generated answers.

**Key features:**
- **Analysis mode selection** — guides the user to enable browser access (Claude in Chrome) for full page inspection, or transparently explains limitations of web fetch mode
- **Entity graph approach** — builds connected entities across pages using `@id` references, not isolated markup per page
- **AEO properties** — `Speakable`, `knowsAbout`, `sameAs` strategy, author-as-Person for LLM attribution
- **Existing markup detection** — finds and fixes current schema before generating new markup (requires browser mode)
- **Platform-specific instructions** — Tilda, WordPress, Shopify, Webflow, React/Next.js, GTM
- **Clean JSON output** — delivers `.json` files ready for any CMS

## Installation

### Option 1: Copy to Claude.ai (simplest)

1. Download `SKILL.md` from `skills/schema-markup/`
2. Paste its contents at the beginning of your Claude.ai conversation
3. Ask Claude to create or fix schema for your page

### Option 2: Install as a user skill

Copy the `skills/schema-markup/` folder to your skills directory:

```
.agents/skills/schema-markup/
├── SKILL.md
├── references/
│   └── schema-examples.md
└── evals/
    └── evals.json
```

### Option 3: Claude Code / SkillKit

```bash
npx skills add https://github.com/YOUR-USERNAME/schema-markup-skill --skill schema-markup
```

## Usage

Just ask Claude naturally:

- "Create schema markup for https://example.com"
- "Add structured data to my product page"
- "Fix the JSON-LD on my homepage"
- "I need FAQ schema for this page"
- "Improve my site's entity graph for AI visibility"
- "Add Speakable markup to my blog posts"

Claude will first ask you to choose an analysis mode (browser / web fetch / manual), then inspect your page, and generate complete JSON-LD markup.

## Schema types covered

| Type | Use case |
|------|----------|
| Organization | Company homepage, about page |
| WebSite | Homepage with search |
| Article / BlogPosting | Blog posts, news, guides |
| Product | Product and service pages |
| SoftwareApplication | SaaS, apps |
| FAQPage | FAQ sections on any page |
| HowTo | Tutorials, step-by-step guides |
| BreadcrumbList | All pages (navigation path) |
| LocalBusiness | Local business pages |
| ItemList / CollectionPage | Category and listing pages |

## AEO features

Traditional schema targets Google rich results. This skill additionally optimizes for AI answer engines:

- **Speakable** — marks content sections suitable for AI quotation and voice readout
- **knowsAbout** — signals topical expertise to LLMs building authority models
- **sameAs strategy** — connects entities to Wikipedia, Wikidata, social profiles for Knowledge Panel and AI entity resolution
- **Entity graph** — `@id` linking across pages so AI systems understand the full picture of your brand
- **Author as Person** — full Person entities with `jobTitle`, `worksFor`, `sameAs` for proper E-E-A-T attribution

## File structure

```
skills/schema-markup/
├── SKILL.md                          # Main skill instructions (406 lines)
├── references/
│   └── schema-examples.md            # Complete JSON-LD examples for 9 page types
└── evals/
    └── evals.json                    # Test scenarios for skill validation
```

## Created by

Yulia Glukhova — founder of [Far and Wide](https://www.farandwide.io/), an AEO-agency helping brands rank #1 when customers ask AI for solutions.

## License

MIT
