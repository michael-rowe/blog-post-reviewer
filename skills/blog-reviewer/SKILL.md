| name | blog-reviewer |
| description | Structured four-pass review of a blog post draft: structural framework, voice and style, copy editing, and SEO. TRIGGER when the user wants to review or improve a blog post draft before publishing. Reads config.md for audience, dialect, and style preferences. |
| allowed-tools | Agent, Read |
| argument-hint | path to draft file |

# Blog post reviewer

You orchestrate a structured four-pass review of a blog post draft. Each pass is
handled by a specialist agent. You synthesise their findings into a single set of
priority actions.

## Setup

1. **Read config.md** from the repository root if it exists. Note the audience,
   dialect, platform, and style settings — you will pass these to each agent.
   If config.md is missing or a field is blank, agents use their defaults.

2. **Read the draft** at the path provided in $ARGUMENTS. If no path was provided,
   ask: "What draft should I review?" Read the full content before proceeding.

3. **Check for field-note posts**: if the draft has `subtype: field-note` in its
   frontmatter, pass this to the structural-reviewer and skip the style-reviewer.
   Field notes only need structural (signal-to-noise and audience utility only)
   and SEO passes.

---

## Review pipeline

Run all applicable agents in parallel. Pass each agent the full draft content and
the config settings as context in your instructions.

### Pass 1 — Structural review
Spawn the `structural-reviewer` agent. Include the full draft text and any config
settings (audience, dialect) in the instructions.

### Pass 2 — Style and voice review
Spawn the `style-reviewer` agent. Include the full draft text and any style notes
from config. Skip this pass for field-note posts.

### Pass 3 — Copy editing
Spawn the `copy-editor` agent. Include the full draft text and the dialect setting
from config (default: British English).

### Pass 4 — SEO
Spawn the `seo-optimiser` agent. Include the full draft text, any keyphrase from
the frontmatter, and the platform setting from config.

---

## Synthesis

After all agents have returned their findings, produce a single consolidated report:

### 1. Overall verdict (3–4 sentences)
What the post does well. The single most important structural issue. Whether it is
ready to publish or needs work first.

### 2. Structural findings
Summarise the structural-reviewer's output. Highlight the macro-structure verdict
and the top 2–3 structural issues.

### 3. Voice and style findings
Summarise the style-reviewer's output. Highlight the top 2 issues.
(Omit for field-note posts.)

### 4. Copy editing findings
Summarise the copy-editor's output. Highlight patterns to address and publication
readiness verdict.

### 5. SEO findings
Summarise the seo-optimiser's output. Include the recommended keyphrase and top
metadata gaps.

### 6. Priority actions
A single consolidated list of the 5–7 most important changes across all four passes,
ordered by impact. Where agents flagged the same issue, merge into one action.
Number them — these are the actions the author should take, in sequence.
