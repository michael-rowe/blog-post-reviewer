# Blog post reviewer

A Claude Code skill for structured review of blog post drafts.

Most writing tools help you write. This one helps you evaluate what you have written
— before you publish it.

The skill applies a seven-point structural framework to any blog post draft, checking
macro-architecture, narrative momentum, signal-to-noise ratio, signposting quality,
visual ergonomics, cross-section coherence, and resolution. It returns a prioritised
list of changes, not a rewrite.

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
claude plugin marketplace add https://github.com/michael-rowe/blog-post-reviewer
claude plugin install blog-post-reviewer@michael-rowe-blog-post-reviewer
```

## Usage

```bash
/blog-reviewer path/to/draft.md
```

The skill reads your draft, applies the framework, and returns structured feedback
with a priority actions list.

## Configuration

After installation, edit `config.md` to personalise the review:

- **Audience** — who you are writing for; the reviewer checks whether content
  serves them
- **Dialect** — British English or American English (default: British English)
- **Serial comma** — yes or no (default: yes)
- **Platform** — where you publish; affects metadata and linking guidance
- **Style notes** — any voice or register preferences

Leave any field blank to use the defaults.

## What the skill checks

| Criterion | What it asks |
| --------- | ------------ |
| Macro-structure | Is the architecture matched to the content type? |
| Narrative velocity | Does the opening create a curiosity gap? Does every element pull the reader forward? |
| Signal-to-noise | Has everything irrelevant or redundant been removed? |
| Signposting | Are transitions smooth? Is there balance across logical move types? |
| Visual ergonomics | Does it pass the Layer Cake test (headings alone tell the story)? The F-Pattern test (key words at the start of sentences)? |
| Cross-section coherence | Does the same idea appear in different words across sections? |
| Resolution | Does the conclusion resolve or repeat? |
| Audience utility | Is there a clear foothold for the reader? |

## Supported macro-structural frameworks

The skill recognises and evaluates against these frameworks:

| Framework | Best for |
| --------- | -------- |
| Inverted Pyramid | Updates, announcements, news |
| PAS (Problem-Agitate-Solve) | How-to, opinion, persuasion |
| SCQA (Situation-Complication-Question-Answer) | Technical explanation, analysis |
| STARR (Situation-Task-Action-Result-Reflection) | Case studies, personal experience |
| BAB (Before-After-Bridge) | Transformation posts, "how I changed my mind" |
| Monroe's Motivated Sequence | Advocacy, calls to action |
| Hero's Journey | Personal growth narratives |

## This skill as part of a wider workflow

This skill covers structural review — the first pass on a draft. A complete blog
post review workflow also benefits from:

- **Voice and style review**: checking analytical positioning, conceptual habits,
  and sentence-level patterns
- **Copy editing**: British conventions, sentence-level clarity, grammar
- **SEO review**: keyphrase strategy, metadata, internal linking

These are separate concerns with separate review criteria. Combining them into a
single pass produces shallower feedback on each.

## Contributing

Pull requests are welcome. The most useful contributions are:

- Additional macro-structural frameworks with clear use cases
- Improvements to the signposting taxonomy
- Refinements to the visual ergonomics checks
- Fixes to ambiguous or unclear criteria

Please open an issue before submitting large changes to discuss the approach first.

## License

MIT
