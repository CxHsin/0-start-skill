# 0-start Skill Design

## Summary

`0-start` is a skill for helping a user enter an unfamiliar field without pretending to teach the whole field from scratch. Its job is to establish a reliable first impression as quickly as possible by starting from real hiring language, extracting core terms, recommending a small set of high-signal first-party sources, answering follow-up questions, and only then suggesting a learning path.

The skill is intentionally not a generic beginner explainer, not a one-shot course generator, and not a broad content dump. It acts as a cold-start coach for a new domain.

## Goals

- Help the user form a trustworthy first impression of a field.
- Use JD-style market signals to ground the explanation in real-world demand.
- Introduce a small vocabulary set so the user stops feeling lost when seeing field-specific terms.
- Recommend a few high-quality first-party sources instead of overwhelming the user.
- Stay in follow-up Q&A mode until the user has enough structure to benefit from a learning path.
- Provide a high-quality learning route only after that first impression exists.

## Non-Goals

- Fully teaching a field from zero in one interaction.
- Producing a long curriculum immediately.
- Leading with low-signal secondary summaries as core material.
- Pretending there is one unified answer when the field actually has multiple sub-branches.
- Optimizing for exhaustiveness over clarity.

## Primary User Flow

1. The user provides only a field or direction name, such as `I want to learn Agent Engineer`.
2. The skill derives representative JD signals for that field and extracts recurring tasks, tools, and capability language.
3. The skill presents a light first response containing:
   - a brief JD signal overview
   - 5 to 8 core terms with plain-language explanations
   - 3 to 5 high-quality first-party sources
   - one concrete next step
4. The skill answers follow-up questions, especially around:
   - terminology
   - relationships between tools, frameworks, and workflows
   - what to read first and what to ignore
5. Once the user has formed a first impression, the skill either offers or provides a high-quality learning route.

## Inputs

### Required Input

- A field or direction name from the user.

Examples:

- `I want to learn AI Agent Engineer`
- `I want to learn quant research`
- `I want to learn growth`

### Optional Follow-Up Context

The skill may ask one lightweight follow-up question if it would materially improve relevance. Typical examples are:

- whether the user is exploring for jobs, projects, or general understanding
- whether the user is completely new, has adjacent background, or has already read a little

This is optional and must not block the primary flow. If the answer would not clearly change the output, the skill should skip the question.

## Outputs

### First Response Output Shape

The first response should stay intentionally light and high-signal. It should include four sections.

### 1. JD Signal Snapshot

A short summary of what this field looks like in hiring language:

- recurring responsibilities
- common tools or frameworks
- notable capability patterns

This section should help the user understand how the market describes the field. It should emphasize stable, reusable patterns rather than short-lived hype.

### 2. Core Term Cards

Five to eight high-frequency terms with one plain-language explanation each. The purpose is not full rigor. The purpose is to prevent the user from bouncing off the field's vocabulary on first contact.

These term cards should focus on stable core concepts. Short-cycle buzzwords or currently fashionable tool names should not dominate the first response.

### 3. First-Party Source Entry Points

Three to five recommended sources. Each recommendation must include:

- why it is worth reading
- what kind of understanding it helps build
- where the user should start

### 4. Next Best Step

One concrete action for the user, such as reading one or two recommended sources and returning with questions about terminology or relationships.

### Follow-Up Output Shape

After the first response, the skill should switch into targeted support rather than regenerate another full overview. Follow-up outputs mainly fall into three categories.

### 1. Term Explanation

Clarify the meaning of one term and how it differs from adjacent concepts.

### 2. Relationship Mapping

Explain how tools, frameworks, expectations, or workflows relate to one another in the field.

### 3. Reading Navigation

Help the user choose what to read first, what to defer, and what content is mostly noise.

### Final Output Shape

Once the user has formed a first impression, the skill produces a learning path. The learning path should be staged and concise rather than exhaustive, for example:

- build vocabulary
- read first-party materials to understand the field's main pattern
- complete one minimal practice task
- backfill more systematic knowledge

The learning path should clearly build on the user's current level of understanding rather than reset the conversation.

## Control Logic

### Definition of "First Impression Established"

The skill should treat the user as having formed a first impression when at least two of the following are true:

1. The user asks questions that connect terms rather than only asking `what is this`.
2. The user shows a rough understanding of the field's typical work, not just isolated tools.
3. The user has engaged with at least some first-party material and can report what made sense or where they got stuck.

### Default Behavior Before That Point

Before these signals are present, the skill should continue answering questions and narrowing the information surface. It should not rush into a learning path.

### Transition to Learning Path

The transition can happen in two ways:

#### Explicit Trigger

The user directly asks for a learning route.

#### Implicit Trigger

The skill observes that the user likely has a first impression and offers a choice such as:

`You should now have a rough first impression of this field. I can either keep helping you unpack terms and source material, or I can turn this into a high-quality learning path.`

### Negative Rule

If the user asks many questions but still appears stuck at a repetitive and very basic level, the skill should not force progress into the learning-path phase. It should reduce jargon, reduce source count, and continue to strengthen the user's mental model first.

## JD Signal Acquisition

The skill should use a hybrid JD acquisition strategy.

### Preferred Strategy

- Prefer recent, real, attributable hiring signals.
- Source priority for JD-style evidence should generally be:
  - company careers pages
  - official team or role descriptions published by the company
  - high-credibility job platforms when primary sources are unavailable

### Hybrid Fallback

If recent JD evidence is thin, the skill may supplement with relatively stable field-level consensus to help the user form a first impression.

### Output Transparency

When the field is fast-moving, the skill should clearly distinguish between:

- recent hiring signals
- more stable field-level patterns

The skill should not present unstable market language as timeless fact.

### Copyright and Quotation Rule

The skill should not reproduce full JD text. It should extract and paraphrase recurring tasks, terminology, tools, and capability expectations.

## Source Selection Rules

### Core Principle

The skill should prioritize whichever sources are most first-hand, most reality-linked, and least diluted for the field in question. It should not assume that every field has an "official docs" layer.

### JD Selection

The skill should use JD-style evidence to extract representative market language. It does not need large-scale coverage. It needs enough signal to identify recurring terminology, tools, tasks, and capability expectations.

When different JDs disagree, the skill should not flatten them into a false single story. Instead, it should explain that the field may contain branches or competing conventions.

### Source Priority

Source selection should adapt to the field, using this general priority:

1. first-hand authority sources in that field
2. direct practitioner output
3. high-credibility structured explanation

Examples of first-hand authority sources may include:

- official documentation or official blogs
- author blogs, maintainer notes, or project homepages
- official team pages or role descriptions
- original frameworks, standards, or institutional publications

Examples of direct practitioner output may include:

- engineering blogs
- operator writeups
- practitioner case studies
- experienced professionals' long-form explanations

Examples of high-credibility structured explanation may include:

- strong papers
- technical reports
- industry research
- a small amount of high-quality secondary explanation when needed

If a field does not have an official documentation layer, the skill should automatically fall back to the strongest available first-hand practice sources instead of forcing a technical template.

### Source Presentation Rules

The skill must not only provide links. For each recommended source, it should state:

- what signal makes it trustworthy
- what kind of understanding it helps establish
- what the user should start with

### Avoidance Rules

- Do not treat SEO aggregation pages as core sources.
- Do not use obvious repost chains or diluted rewrites as first-impression anchors.
- Do not sacrifice truth for superficial accessibility.
- Do not push source-selection burden onto the user when the skill can narrow it to 3 to 5 strong starting points.

### Stability Rule for Beginners

The first response should prioritize stable, reusable, reality-linked information. It should not foreground short-cycle trend information for a beginner.

If a currently popular tool or term appears frequently in JD evidence, the skill may mention it as an example, but it should not present it as the field itself.

Trend-layer explanation should usually be deferred until the user explicitly asks about current waves, common tool choices, or why specific names keep appearing.

## Experience Principles

- Start from reality, not abstract pedagogy.
- Keep the first response light.
- Prefer signal over volume.
- Use first-party material as the main trust anchor.
- Let the user ask concrete questions before prescribing a route.
- Move to a learning path only when the user has enough structure for it to be useful.

## Personalization Rules

### Background Awareness

If the user already reveals background in the initial request, the skill should use it immediately.

Examples:

- `I am a backend engineer and want to learn Agent Engineer`
- `I am completely new and want to understand growth`

If no background is provided, the skill should default to a lightweight neutral first response rather than force extra questions.

### Background Types

Useful background signals include:

1. adjacent background
2. complete beginner
3. partial prior exposure

### How Background Changes Output

Background should materially affect the first response.

- In `JD Signal Snapshot`:
  - adjacent-background users should see transferable skills and key differences
  - complete beginners should see a simpler explanation of what the field is and how it differs from nearby roles
- In `Term Cards`:
  - adjacent-background users should get less explanation of shared concepts and more explanation of field-specific concepts
  - complete beginners should get plainer language and fewer assumed prerequisites
- In `Source Recommendation`:
  - adjacent-background users can be moved more quickly into strong first-party material
  - complete beginners should still get first-party sources, but with gentler starting points
- In `Next Best Step`:
  - adjacent-background users can be pointed toward contrastive reading or early practice
  - complete beginners should first build vocabulary and structure

### Goal-Based Personalization

If the skill asks whether the user is exploring for jobs, projects, or general understanding, the answer must change the output.

- job-focused users should get stronger emphasis on responsibilities, hiring language, and role expectations
- project-focused users should get stronger emphasis on task flow, tool combinations, and minimal practical execution
- understanding-focused users should get stronger emphasis on concept map, vocabulary, and field structure

### Ask-Only-If-Useful Rule

If a follow-up answer would not materially change:

- `JD Signal Snapshot`
- `Term Cards`
- `Source Recommendation`
- `Next Best Step`

then the skill should not ask the question.

## Recommended Initial Version

The first shipped version should be the basic version only. It should cover:

- JD signal extraction
- term cards
- first-party source recommendation
- Q&A continuation
- learning-path output

It should not yet include elaborate background-based branching or heavyweight evidence reporting. Those can be future extensions if the basic flow proves useful.

## Example First Responses

The following examples are intended to validate tone, depth, and structure. They should feel light, grounded, and useful for a beginner, not encyclopedic.

### Example A: `I want to learn Agent Engineer`

#### JD Signal Snapshot

If you read current Agent Engineer-style job descriptions, the stable pattern is usually not "just use a specific framework." The job is more often described as:

- building task flows around LLMs
- connecting models to tools, APIs, data, and memory
- improving reliability, evaluation, and debugging
- turning vague AI demos into repeatable product or internal workflows

So the stable core is not one hot tool. It is the ability to design, connect, observe, and improve LLM-powered workflows.

#### Core Term Cards

- `tool calling`: letting the model use external tools or APIs instead of only generating text
- `workflow`: the multi-step path that the model and surrounding system follow to complete a task
- `evaluation`: checking whether the system is actually doing the right thing, not just sounding plausible
- `memory`: what the system keeps across steps or sessions to stay coherent
- `orchestration`: coordinating models, tools, and control logic into a usable flow
- `guardrails`: constraints and checks that reduce failure or unsafe behavior

#### First-Party Source Entry Points

- OpenAI platform docs or official guides
  Good for seeing the stable building blocks directly from a primary source. Start with the sections on tool use, workflows, and evaluation.
- Anthropic engineering or product documentation
  Useful for understanding how another major model provider frames agents, tools, and safety. Start with agent- or tool-related guides rather than model marketing pages.
- LangGraph or similar project documentation
  Useful as an example of how workflow orchestration is implemented in practice. Read it as one possible implementation layer, not as the field itself.

#### Next Best Step

Pick two first-party sources above and read only enough to answer this question: `What stays the same across these systems, even if the framework names differ?` Then come back and ask me about any terms or relationships that still feel fuzzy.

### Example B: `I want to learn growth`

#### JD Signal Snapshot

If you read growth-related roles, the stable pattern is usually not "know a few marketing tricks." The role is more often described as:

- finding where users drop off or fail to activate
- running experiments to improve acquisition, activation, retention, or monetization
- using data to locate bottlenecks and measure change
- connecting product behavior, messaging, and distribution into a repeatable improvement loop

So the stable core is not a channel hack. It is the ability to identify leverage points in a user journey and improve them with disciplined testing.

#### Core Term Cards

- `activation`: the moment a user reaches initial value from the product
- `retention`: whether users keep coming back over time
- `funnel`: the step-by-step path users take from awareness to ongoing usage
- `experiment`: a structured test to learn whether a change improves an outcome
- `conversion`: the rate at which users move from one stage to the next
- `north star metric`: a key metric used to reflect meaningful product value

#### First-Party Source Entry Points

- Reforge-style original long-form essays or frameworks from experienced operators
  Useful for building a structured sense of how growth work is framed in practice. Start with activation, retention, or experimentation pieces.
- Public growth or product writeups from strong companies
  Useful because they show how real teams diagnose bottlenecks and test changes. Start with case studies that explain the problem, intervention, and measurement.
- Original practitioner essays from experienced growth leaders
  Useful for understanding the judgment behind growth work, not just the vocabulary. Prefer pieces that explain tradeoffs and process over "10 hacks" content.

#### Next Best Step

Read one piece about activation and one about retention, then come back and tell me which one feels more concrete to you. I can use that to help you build the rest of the field map without overwhelming you.
