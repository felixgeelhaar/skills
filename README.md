# Claude Code Expert Skills

A collection of expert-level skills for [Claude Code](https://claude.ai/code) that act as senior thinking partners across product, engineering, design, AI, and go-to-market disciplines.

Each skill brings deep domain knowledge grounded in named practitioners and frameworks, operates through Socratic questioning, and cross-references the others to form an integrated advisory network.

## Skills

| Skill | Role | Grounded In |
|-------|------|-------------|
| [**engineering-expert**](./engineering-expert/) | Architecture evaluation, trade-off analysis, system design review | Fowler, Martin, Evans, Newman, Hohpe, Richards & Ford, Nygard, Beck, Kleppmann, Bass/Clements/Kazman, Forsgren/Humble/Kim |
| [**product-expert**](./product-expert/) | Product strategy, discovery, roadmapping, OKRs | Cagan, Cutler, Perri, Torres, Eriksson, Rachitsky, Doshi, Biddle, Singer, Wardley |
| [**ux-expert**](./ux-expert/) | UX research, psychology laws, accessibility, design systems | Norman, Krug, Walter, Goodwin, Wroblewski, Spool, Holmes, Frost |
| [**ai-expert**](./ai-expert/) | AI product design, model selection, evals, responsible AI | Mollick, Ng, Huyen, Yan, Swyx, Willison, Husain |
| [**gtm-expert**](./gtm-expert/) | Go-to-market strategy, positioning, pricing, launch | Voje, Dunford, Bush, Lochhead, Vajre, Poyar, Gerhardt, Ulwick |

## How They Work Together

The skills form a cross-functional advisory network. Each skill knows when to defer to another:

```
                    product-expert
                   /       |       \
            ux-expert  ai-expert  gtm-expert
                   \       |       /
                  engineering-expert
```

- **engineering-expert** evaluates architecture and invokes `/product-expert` for business context, `/ux-expert` for user impact, `/ai-expert` for AI-specific decisions
- **product-expert** drives strategy and invokes `/ux-expert` for design thinking, `/gtm-expert` for market strategy, `/ai-expert` for AI feature evaluation
- **ux-expert** reviews interfaces and invokes `/product-expert` for prioritization, `/ai-expert` for AI UX patterns
- **ai-expert** evaluates AI architecture and invokes `/product-expert` for strategy, `/ux-expert` for AI UX review
- **gtm-expert** plans go-to-market and invokes `/product-expert` for positioning alignment

## Operating Modes

Every skill supports multiple modes of engagement:

| Mode | What It Does | Example Prompt |
|------|-------------|----------------|
| **Socratic Evaluator** | Questions before judging, surfaces assumptions | "Review this architecture for our payment service" |
| **Document Writer** | Produces real artifacts (ADRs, PRDs, briefs) | "Write a product brief for the notification system" |
| **Decision Challenger** | Compares options with explicit trade-offs | "Should we use event sourcing or CRUD for audit logs?" |
| **Pairing Partner** | Invokes other skills when cross-discipline | "Is this the right UX for our AI feature?" |

## Installation

### Option 1: Install Individual Skills

Copy a specific skill into your Claude Code skills directory:

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/<skill-name>

# Copy the skill file
cp <skill-name>/SKILL.md ~/.claude/skills/<skill-name>/SKILL.md
```

### Option 2: Install All Skills

```bash
# Clone the repository
git clone https://github.com/felixgeelhaar/skills.git /tmp/claude-skills

# Copy all skills
for skill in ai-expert engineering-expert gtm-expert product-expert ux-expert; do
  mkdir -p ~/.claude/skills/$skill
  cp /tmp/claude-skills/$skill/SKILL.md ~/.claude/skills/$skill/SKILL.md
done
```

### Option 3: Symlink (for Development)

```bash
# Clone to a permanent location
git clone https://github.com/felixgeelhaar/skills.git ~/Developer/skills

# Symlink each skill
for skill in ai-expert engineering-expert gtm-expert product-expert ux-expert; do
  ln -sf ~/Developer/skills/$skill ~/.claude/skills/$skill
done
```

## Usage

Skills activate automatically when Claude Code detects relevant context. You can also invoke them explicitly:

```
/engineering-expert   — Evaluate architecture or technical decisions
/product-expert       — Think through product strategy or write product documents
/ux-expert            — Review interfaces, accessibility, or UX patterns
/ai-expert            — Evaluate AI features, model choices, or AI architecture
/gtm-expert           — Plan go-to-market, positioning, or launch strategy
```

### Example Interactions

**Architecture evaluation:**
> "We're considering moving from a monolith to microservices. Our team is 8 engineers and we serve ~5,000 requests/second."

**Product strategy:**
> "Should we build a self-serve analytics dashboard or invest in our API for power users?"

**UX review:**
> "Review the checkout flow at localhost:3000/checkout for accessibility and conversion."

**AI feature design:**
> "We want to add AI-powered search to our documentation site. What tier of AI product is this?"

**GTM planning:**
> "We're launching a developer tool. Should we go PLG or sales-led?"

## Skill File Format

Each skill follows the Claude Code SKILL.md format:

```yaml
---
name: skill-name
description: >
  Role description with TRIGGER conditions and DO NOT TRIGGER exclusions.
allowed-tools: Read, Glob, Grep, WebSearch, WebFetch, ...
---

# Skill content (Markdown)
- Knowledge base grounded in named thinkers
- Frameworks and mental models
- Operating modes
- Output format templates
```

### Key Design Principles

- **Named thinkers, not generic advice** — Every framework is attributed. No "best practices say..." without a source.
- **Socratic by default** — Skills question before they answer. Assumptions are surfaced, not bypassed.
- **Trade-offs over recommendations** — Every recommendation names what you're giving up.
- **Concrete over abstract** — Quality attributes are scenarios with response measures, not vague "-ilities".
- **Cross-functional by design** — Skills invoke each other at discipline boundaries rather than overstepping.

## Contributing

1. Fork the repository
2. Create a new skill directory: `mkdir my-skill`
3. Add a `SKILL.md` following the format above
4. Ensure TRIGGER and DO NOT TRIGGER conditions are specific
5. Ground the knowledge base in named practitioners and frameworks
6. Include cross-references to existing skills where relevant
7. Submit a pull request

## License

[MIT](./LICENSE)
