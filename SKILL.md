> **同步说明**: 此副本位于 F:\个人\学术写作skill\Skill\lab-paper-polisher，与 C:\Users\Razor\.codex\skills\lab-paper-polisher（Codex自动发现位置）保持同步。更新时需同时更新两处。
>
---
name: lab-paper-polisher
description: Polish English academic paragraphs with sentence-structure diversity, research-group style alignment, and detailed revision explanations. Use when Codex needs to (1) polish English academic paragraphs for journal-readiness, (2) optimize sentence structure diversity to avoid repetitive patterns, (3) align writing with a specified research group's academic style, (4) provide detailed revision explanations with style basis, or (5) reduce AI-generation traces in academic prose. This skill performs language-level optimization only: it does not change the user's core academic arguments, experimental data, or research conclusions. It does not generate full papers, expand, or condense content.
---

# Lab Paper Polisher

## Overview

This skill refines English academic prose written by non-native speakers or AI-assisted drafting into publication-ready language. It preserves every factual claim and structural intention of the original while improving lexical precision, syntactic variety, idiomatic flow, and conformity to the target research community's stylistic conventions.

## When This Skill Applies

The core scenario: a user pastes one or more English academic paragraphs and asks for language polishing, sentence restructuring, or style alignment. Variants include:

- "Polish this paragraph so it sounds more like native academic English."
- "Rewrite to vary the sentence openings."
- "Make this match the writing style of our group."
- "Explain what you changed and why."
- "Reduce the AI-sounding phrasing in this methodology section."

If the user asks for generation of full papers, expansion/summarization of content, or changes to data/claims, do not apply this skill.

## Workflow

### Step 1: Load style references (if available)

Before touching any text, check the `references/` directory for available writing-style profiles. The user may have stored sample paragraphs, style guides, or previously polished content there.

- If the user names a specific principal investigator, lab, journal, or writing style, search the references for a matching file and read it into context.
- If no specific style is named but files exist in `references/`, ask the user which profile to follow, or whether to use general academic English conventions.
- If the `references/` directory is empty or no style is specified, default to general best practices in academic English writing.

### Step 2: Analyze the input paragraph

Read the user's text and identify the following without outputting an intermediate analysis:

- Repeated sentence structures or rhythmic patterns (e.g., every sentence starting with "We found that...")
- Awkward or non-idiomatic phrasing that signals non-native construction or AI generation
- Heavy nominalizations, passive overuse, or convoluted clause stacking
- Inconsistent terminology, register mismatches, or discipline-inappropriate word choices
- Overused academic filler (notably, importantly, interestingly, it is worth noting that)

Decide which issues to address and which to leave untouched based on the user's request. If the user only asked for sentence-structure diversity, do not perform a full vocabulary overhaul.

### Step 3: Rewrite

Produce the revised paragraph(s) following the modification rules below. The output must read as natural academic prose written by a fluent scholar in the field.

Apply changes at the sentence level: vary openings, alternate between active and passive voice where appropriate, break or combine clauses for rhythm, replace formulaic transitions with substantive connectors, and prefer concrete verbs over nominalized constructions.

### Step 4: Provide structured revision notes

After the revised text, append a clear revision log following the structure below.

## Output Format

The output always consists of two sections separated by a blank line:

### Revised paragraph

Present the full polished paragraph. If multiple paragraphs were given, present each with a clear label.

### Revision Notes

The notes must follow this structure:

| Original | Revised | Category | Rationale |
|----------|---------|----------|----------|
| The original phrase or sentence | The revised phrase or sentence | One of: Vocabulary, Sentence Structure, Tone/Register, Academic Convention, Conciseness, Clarity, Style Alignment | Why the change was made, including reference to the group style guide (if applicable) or general academic writing principle |

**Category definitions:**
- **Vocabulary**: Word choice, terminology precision, collocation
- **Sentence Structure**: Word order, clause arrangement, sentence combining/splitting, opening variation
- **Tone/Register**: Formality level, hedging strength, modality
- **Academic Convention**: Discipline-specific formatting, citation style, field norms
- **Conciseness**: Removal of wordiness, redundant modifiers, filler phrases
- **Clarity**: Ambiguity resolution, pronoun reference, logical flow
- **Style Alignment**: Specific alignment with a lab/writing style from references/

**Guidelines for the table:**
- Include 3-8 representative changes. Do not list every trivial change (e.g., article fix) unless the user specifically asked for exhaustive tracking.
- Prioritize changes that (a) involved judgment calls, (b) directly address the user's request, or (c) reflect the group's style.
- When the user specified a style profile, every Rationale entry that reflects that style must mention the profile name and specific stylistic rule.

## Modification Rules

### Must do

- Vary sentence openings and structures to break repetitive patterns.
- Replace obviously AI-generated phrasings (e.g., "a myriad of," "in the realm of," "it is imperative to," "delved into," "shed light on," "a wealth of," "overarching," "in recent years, there has been") with natural academic equivalents.
- Prefer concrete, field-specific verbs over generic ones.
- Replace weak hedging ("may potentially," "could possibly") with precise epistemic qualification.
- Eliminate wordy filler: "it should be noted that," "it is worth mentioning that," "as a matter of fact."
- Break up chains of prepositional phrases or stacked relative clauses.
- Prefer active voice for methodology actions done by the authors, passive voice for established knowledge or unknown agents.
- Fix article errors (a/an/the), subject-verb agreement, and preposition choice as needed.

### Must not do

- Do not change any factual content, numerical data, chemical formula, statistical result, or citation.
- Do not add new claims, interpretations, or conclusions.
- Do not remove or add hedging that would change the epistemic strength of a claim.
- Do not reorganize paragraphs or change the order of presented arguments.
- Do not expand a short phrase into a longer explanation, or condense a detailed description.
- Do not change discipline-specific technical terms to generic synonyms.
- Do not apply the same transformation across every sentence, aim for natural variation.

### When to leave text untouched

- A sentence that already reads naturally and idiomatically in academic English: leave it.
- Technical terminology and equations: leave them.
- Established field-specific phrasings: leave them unless the user specifically asks.
- Short, clear sentences that serve a rhetorical purpose: leave them.

## Writing Style Profiles (references/)

The `references/` directory stores one or more writing-style profiles. A pre-built style profile `references/environmental-engineering-style.md` is already available, covering vocabulary, sentence structure, paragraph logic, tone, and discipline-specific conventions for the environmental engineering / water research field. Load this profile when the user asks for alignment with this discipline's writing conventions. Additional profiles can be created from sample texts.

A profile file typically contains:
- Sample paragraphs from the group's published papers marked with stylistic annotations
- Recurring syntactic patterns and preferred constructions
- Vocabulary preferences and dispreferred terms
- Common tics or errors to avoid

### Adding a new style profile

When the user provides additional sample texts for style profiling:

1. Analyze 2-3 sample paragraphs from the group's published papers (user-provided).
2. Extract a reusable style profile: identify 5-15 concrete, actionable stylistic features (sentence-opening preferences, passive/active balance, technical noun-phrase density, hedging patterns, transition strategies, punctuation habits, etc.).
3. Write the profile as a markdown file in `references/`, named with the lab name or PI name in kebab-case (e.g., `prof-wang-style.md`, `zhang-lab-style.md`).
4. Each profile must include:
   - A one-sentence identifying header
   - A list of characteristic stylistic features with examples from the samples
   - A list of dispreferred patterns to avoid
5. Update this SKILL.md `Writing Style Profiles` section if the skill description becomes stale.

