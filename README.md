# Expert Skills for AI Coding Agents

A collection of 13 expert-level skills for AI coding agents that act as senior thinking partners across engineering, product, design, data, security, operations, growth, and business disciplines.

Each skill brings deep domain knowledge grounded in named practitioners and frameworks, operates through Socratic questioning, and cross-references the others to form an integrated advisory network. The skills are agent-agnostic — they work with any AI coding agent that supports system prompt injection or skill files (Claude Code, Cursor, Windsurf, Cline, Aider, etc.).

## Skills

### Build

| Skill | Role | Grounded In |
|-------|------|-------------|
| [**engineering-expert**](./engineering-expert/) | Architecture evaluation, trade-off analysis, system design | Fowler, Martin, Evans, Newman, Hohpe, Richards & Ford, Nygard, Beck, Kleppmann, Bass/Clements/Kazman, Forsgren/Humble/Kim |
| [**ux-expert**](./ux-expert/) | UX research, psychology laws, accessibility, design systems | Norman, Krug, Walter, Goodwin, Wroblewski, Spool, Holmes, Frost |
| [**ai-expert**](./ai-expert/) | AI product design, model selection, evals, responsible AI | Mollick, Ng, Huyen, Yan, Swyx, Willison, Husain |
| [**data-expert**](./data-expert/) | Analytics strategy, experimentation, data modeling, governance | Rogati, Patil, Kohavi, Thomke, Kimball, Dehghani, Handy |
| [**content-expert**](./content-expert/) | Technical writing, docs strategy, developer relations | Procida, Halvorson, Handley, Thengvall, Corleissen |

### Operate

| Skill | Role | Grounded In |
|-------|------|-------------|
| [**devops-expert**](./devops-expert/) | SRE, platform engineering, observability, CI/CD | Kim, Humble, Farley, Majors, Skelton & Pais, Rosenthal, Beyer |
| [**security-expert**](./security-expert/) | Threat modeling, AppSec, compliance, incident response | Shostack, Anderson, Schneier, Janca, Kindervag, McGraw |
| [**legal-expert**](./legal-expert/) | Privacy law, licensing, AI regulation, compliance | Meeker, Mitchell, EU AI Act, GDPR, SOC2, HIPAA |

### Scale

| Skill | Role | Grounded In |
|-------|------|-------------|
| [**product-expert**](./product-expert/) | Product strategy, discovery, roadmapping, OKRs | Cagan, Cutler, Perri, Torres, Eriksson, Rachitsky, Doshi, Biddle, Singer, Wardley |
| [**gtm-expert**](./gtm-expert/) | Go-to-market strategy, positioning, pricing, launch | Voje, Dunford, Bush, Lochhead, Vajre, Poyar, Gerhardt, Ulwick |
| [**growth-expert**](./growth-expert/) | Activation, retention, experimentation, growth loops | Chen, Ellis, Balfour, Kohavi, Bush, Eyal, Fogg |
| [**finance-expert**](./finance-expert/) | Unit economics, pricing models, SaaS metrics, revenue | Skok, Lemkin, Campbell, Ramanujam, Tringas, FinOps |
| [**people-expert**](./people-expert/) | Team topologies, org design, engineering leadership | Skelton & Pais, Larson, Fournier, Reilly, Lencioni, Pink |

## How They Work Together

The skills form a cross-functional advisory network. Each skill knows when to defer to another:

```
                         product-expert
                        /    |    |    \
                 ux-expert   |  gtm-expert
                    |        |       |     \
                ai-expert    |  growth-expert
                    |        |       |
               data-expert   |  finance-expert
                  |    \     |     /
           engineering-expert |   /
                  |      \   |  /
             devops-expert  people-expert
                  |
           security-expert ── legal-expert
```

**Build flow:**
- `engineering-expert` evaluates architecture, defers to `product-expert` for business context, `ux-expert` for user impact, `ai-expert` for AI decisions, `data-expert` for data modeling
- `ux-expert` reviews interfaces, defers to `product-expert` for prioritization, `ai-expert` for AI UX patterns
- `ai-expert` evaluates AI architecture, defers to `engineering-expert` for system design, `data-expert` for data pipelines
- `data-expert` reviews analytics and experimentation, defers to `engineering-expert` for infrastructure, `product-expert` for metric definitions
- `content-expert` reviews docs and writing, defers to `ux-expert` for information architecture, `engineering-expert` for API docs

**Operate flow:**
- `devops-expert` evaluates infrastructure, defers to `engineering-expert` for architecture, `security-expert` for hardening
- `security-expert` threat-models systems, defers to `engineering-expert` for design review, `legal-expert` for compliance
- `legal-expert` assesses legal risk, defers to `security-expert` for technical controls, `data-expert` for data governance

**Scale flow:**
- `product-expert` drives strategy, defers to `ux-expert` for design, `gtm-expert` for market, `ai-expert` for AI features
- `gtm-expert` plans go-to-market, defers to `product-expert` for positioning, `growth-expert` for activation
- `growth-expert` designs growth loops, defers to `data-expert` for experimentation, `ux-expert` for onboarding, `finance-expert` for unit economics
- `finance-expert` models the business, defers to `product-expert` for pricing strategy, `gtm-expert` for revenue model
- `people-expert` designs org structure, defers to `engineering-expert` for Conway's Law alignment, `devops-expert` for platform team design

## Operating Modes

Every skill supports multiple modes of engagement:

| Mode | What It Does | Example Prompt |
|------|-------------|----------------|
| **Socratic Evaluator** | Questions before judging, surfaces assumptions | "Review this architecture for our payment service" |
| **Document Writer** | Produces real artifacts (ADRs, PRDs, briefs, threat models) | "Write a product brief for the notification system" |
| **Decision Challenger** | Compares options with explicit trade-offs | "Should we use event sourcing or CRUD for audit logs?" |
| **Pairing Partner** | Invokes other skills when cross-discipline | "Is this the right UX for our AI feature?" |

## Installation

### Using with Claude Code

```bash
# Install all skills
git clone https://github.com/felixgeelhaar/skills.git /tmp/expert-skills
for skill in $(ls /tmp/expert-skills/*/SKILL.md | xargs -I{} dirname {} | xargs -I{} basename {}); do
  mkdir -p ~/.claude/skills/$skill
  cp /tmp/expert-skills/$skill/SKILL.md ~/.claude/skills/$skill/SKILL.md
done
```

### Using with Cursor / Windsurf / Other Agents

Copy the content of any `SKILL.md` into your agent's system prompt, rules file, or custom instructions:

- **Cursor**: Add to `.cursorrules` or project-level rules
- **Windsurf**: Add to `.windsurfrules` or workspace instructions
- **Cline**: Add to custom instructions in settings
- **Aider**: Add to `.aider.conf.yml` conventions or use `--read` flag
- **Any agent**: Paste the SKILL.md content as a system prompt or prepend it to your conversation

### Using as Standalone Prompts

Each `SKILL.md` is a self-contained expert prompt. You can use it directly with any LLM:

1. Copy the content after the YAML frontmatter (`---`)
2. Paste it as a system prompt in ChatGPT, Claude, Gemini, or any LLM interface
3. Start asking questions — the skill will guide the interaction

## Usage Examples

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

**Data strategy:**
> "We're tracking 40 metrics but nobody looks at the dashboard. How do we fix our analytics?"

**Security review:**
> "We're adding OAuth to our API. Walk me through the threat model."

**DevOps evaluation:**
> "Our deploys take 45 minutes and we deploy twice a week. How do we get to continuous delivery?"

**Team design:**
> "We're growing from 12 to 30 engineers. How should we structure the teams?"

**Pricing decision:**
> "Should we switch from per-seat to usage-based pricing for our API product?"

**Growth analysis:**
> "Our activation rate is 23%. Where do we start?"

**Docs strategy:**
> "Our docs are outdated and developers complain they can't find anything."

**Legal awareness:**
> "We're collecting user data for an AI feature. What should we be thinking about re: GDPR?"

## Skill File Format

Each skill follows a frontmatter + markdown structure:

```yaml
---
name: skill-name
description: >
  Role description with TRIGGER conditions (when to activate)
  and DO NOT TRIGGER exclusions (when to stay silent).
allowed-tools: Read, Glob, Grep, WebSearch, WebFetch, ...
---

# Skill content (Markdown)
- Knowledge base grounded in named thinkers
- Frameworks and mental models
- Operating modes
- Output format templates
```

The `allowed-tools` field is agent-specific and can be adapted to whatever tool/function calling your agent supports. The core value is in the markdown body — the knowledge base, frameworks, and operating modes.

### Key Design Principles

- **Named thinkers, not generic advice** — Every framework is attributed. No "best practices say..." without a source.
- **Socratic by default** — Skills question before they answer. Assumptions are surfaced, not bypassed.
- **Trade-offs over recommendations** — Every recommendation names what you're giving up.
- **Concrete over abstract** — Quality attributes are scenarios with response measures, not vague "-ilities".
- **Cross-functional by design** — Skills defer to each other at discipline boundaries rather than overstepping.
- **Agent-agnostic** — The knowledge and frameworks work regardless of which AI agent runs them.

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
