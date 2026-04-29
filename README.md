# Blog post reviewer

A Claude Code skill for structured review of blog post drafts.

Most writing tools help you write. This one helps you evaluate what you have written before you publish it.

The skill runs four specialist review agents in parallel — structural, style, copy editing, and SEO — and synthesises their findings into a single priority action list.

## Opinionated by design

This skill reflects one practitioner's view of what makes a blog post work — not a universal standard. The framework, the heuristics, and the defaults are all judgment calls. Use it as a starting point, not a rulebook.

It also makes several assumptions about how you work:

- **Markdown files**: drafts are plain text with optional YAML frontmatter; the skill reads frontmatter fields like `subtype` to adjust its behaviour
- **Claude Code**: the skill runs inside Claude Code and expects `config.md` to be present at the project root (it's optional but read automatically if found)
- **Long-form prose posts**: the framework is designed for substantive standalone posts — not newsletter issues, social media threads, or micro-posts
- **English**: no support for other languages
- **Single-author, personal-register writing**: the audience utility check assumes one author writing in their own voice

### On the style agent

The style reviewer (`agents/style-reviewer.md`) is the most opinionated part of the skill. Its defaults reflect a specific analytical writing philosophy:

- Take clear positions; minimise hedging
- Lead with tension or problem, not solution
- Prefer prose over bullet lists for flowing argument
- Ground abstractions in concrete examples
- End sections with implications, not summaries

These are not universal principles — they are one practitioner's craft commitments. If your writing style or your audience's expectations differ, **edit `agents/style-reviewer.md` directly**. The file is plain markdown. The "Defaults" section is clearly marked — replace or extend it with your own principles. You might:

- Remove the analytical positioning checks if your register is more exploratory
- Replace the "what to flag" list with your own style conventions
- Add a specific voice guide (tone, register, point of view) as a new section

The other agents (structural, copy editing, SEO) are less opinionated and should work without modification for most writers.

## Why a structured review?

Good blog posts fail in predictable ways: the structure doesn't match the content
type, the opening buries the point, the transitions rely on a single logical move
repeated throughout, or the conclusion summarises rather than resolves.

A structured review catches these problems systematically. The framework here is
grounded in cognitive load theory, Joseph Sugarman's Slippery Slide principle, and
the craft practices of writers like Paul Graham and Tim Urban — distilled into a
checklist a reviewer can apply consistently.

## Installation

```bash
gh repo clone michael-rowe/blog-post-reviewer ~/.claude/plugins/blog-post-reviewer
```

Then add the skill to Claude Code by copying the skill file:

```bash
cp ~/.claude/plugins/blog-post-reviewer/skills/blog-reviewer/SKILL.md ~/.claude/commands/blog-reviewer.md
```

Copy the agents directory into your project or a shared location where Claude Code can find them:

```bash
cp -r ~/.claude/plugins/blog-post-reviewer/agents ~/.claude/agents/
```

Copy `config.md` into any project where you want personalised reviews:

```bash
cp ~/.claude/plugins/blog-post-reviewer/config.md ./config.md
```

## Usage

```
/blog-reviewer path/to/draft.md
```

The skill reads your draft, runs four parallel review agents, and returns a
consolidated report with a priority actions list.

## Configuration

Edit `config.md` in your project root to personalise the review:

- **Audience** — who you are writing for; the structural reviewer checks whether content serves them
- **Dialect** — British English or American English (default: British English)
- **Serial comma** — yes or no (default: yes)
- **Platform** — where you publish; affects slug and metadata guidance in the SEO pass
- **Style notes** — voice or register preferences passed to the style reviewer
- **Keyphrase** — if already known, passed directly to the SEO agent

Leave any field blank to use the defaults.

## What the skill checks

### Structural pass

| Criterion | What it asks |
| --------- | ------------ |
| Macro-structure | Is the architecture matched to the content type? |
| Narrative velocity | Does the opening create a curiosity gap? Does every element pull the reader forward? |
| Signal-to-noise | Has everything irrelevant or redundant been removed? |
| Signposting | Are transitions smooth? Is there balance across logical move types? |
| Visual ergonomics | Does it pass the Layer Cake test? The F-Pattern test? |
| Cross-section coherence | Does the same idea appear in different words across sections? |
| Resolution | Does the conclusion resolve or repeat? |
| Audience utility | Is there a clear foothold for the reader? |

### Style pass

| Criterion | What it asks |
| --------- | ------------ |
| Analytical positioning | Does the writing take positions, or hedge? |
| Structural moves | Does it lead with tension, ground abstractions, build to implications? |
| Sentence level | Active voice, nominalisations, paragraph discipline, rhythm |
| What to avoid | Bullet-point defaults, jargon, branded concept names, em-dash overuse |

### Copy editing pass

| Criterion | What it asks |
| --------- | ------------ |
| Dialect and convention | Spelling, punctuation, and house style compliance |
| Grammar and mechanics | Fragments, run-ons, agreement, pronoun reference, parallel structure |
| Clarity and style | Passive voice, nominalisations, redundancy, word economy |
| Heading quality | Case, descriptiveness, parallelism, hierarchy |
| Publication readiness | Ready to publish, or what must change first? |

### SEO pass

| Criterion | What it asks |
| --------- | ------------ |
| Keyphrase strategy | Is the keyphrase realistic and specific? |
| Keyphrase placement | Title, meta description, opening paragraph, subheadings |
| Content structure | Word count, subheading distribution, paragraph length |
| Linking | Internal and external link opportunities |
| Metadata | Title, meta description, slug, tags, author, date |
| Quality signals | Originality, E-E-A-T, readability |

## Supported macro-structural frameworks

The structural agent recognises and evaluates against these frameworks:

| Framework | Best for |
| --------- | -------- |
| Inverted Pyramid | Updates, announcements, news |
| PAS (Problem-Agitate-Solve) | How-to, opinion, persuasion |
| SCQA (Situation-Complication-Question-Answer) | Technical explanation, analysis |
| STARR (Situation-Task-Action-Result-Reflection) | Case studies, personal experience |
| BAB (Before-After-Bridge) | Transformation posts, "how I changed my mind" |
| Monroe's Motivated Sequence | Advocacy, calls to action |
| Hero's Journey | Personal growth narratives |

## Field notes

If your draft has `subtype: field-note` in its frontmatter, the skill applies a
lighter review: structural signal-to-noise and audience utility only, plus the
SEO pass. The style and full structural passes are skipped. A field note can be
two paragraphs — the bar is whether it is worth a reader's thirty seconds.

## Adapting the skill

All agent files are plain markdown in `agents/`. To adapt for your workflow:

- **Change the style defaults**: edit `agents/style-reviewer.md` — the "Defaults" section is clearly marked
- **Change the dialect default**: edit the house style section in `agents/copy-editor.md`
- **Add a macro-structural framework**: add a row to the table in `agents/structural-reviewer.md`
- **Remove a pass entirely**: delete the relevant spawn instruction from `skills/blog-reviewer/SKILL.md`

## Contributing

Pull requests are welcome. The most useful contributions are:

- Additional macro-structural frameworks with clear use cases
- Improvements to the signposting taxonomy
- Refinements to the visual ergonomics checks
- Alternative style defaults for different writing contexts (academic, technical, newsletter)
- Fixes to ambiguous or unclear criteria

Please open an issue before submitting large changes to discuss the approach first.

## License

MIT
