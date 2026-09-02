# Cognitive Accessibility System Prompts: Plain Language & Easy Read

> **Last Updated:** March 30, 2026  
> **Standard:** Based on the Autistic Self Advocacy Network (ASAN) toolkit: *One Idea Per Line: A Guide to Making Easy Read Resources*.

---

## Overview

This repository contains two production-ready system prompts engineered for LLMs (such as Gemini 3.8 Flash) to translate complex source text into cognitively accessible formats:

1. **Plain Language Prompt** — For producing text at a 6th–8th grade reading level using clear, standard paragraph structures.
2. **Easy Read Prompt** — For producing text at a 3rd–5th grade reading level using a strict "one sentence per line" structure paired with literal emoji and icon art placeholders.

Both prompts adhere to the principle of **information integrity**: neither format is a summary. Both versions must communicate the same substantive facts, rights, criteria, and nuances as the technical source material.

---

## Quick Comparison: Plain Language vs. Easy Read

| Feature | Plain Language | Easy Read |
| :--- | :--- | :--- |
| **Primary Audience** | General public, English learners, people with processing difficulties who dislike visual clutter. | People with intellectual and developmental disabilities (IDD), low literacy, or visual learning preferences. |
| **Reading Level** | **6th to 8th grade** | **3rd to 5th grade** |
| **Line & Sentence Flow** | Standard multi-sentence paragraphs connected with conjunctions for smooth rhythm. | **Strictly one sentence per line**; maximum 10–15 words per sentence. |
| **Idea Density** | Multiple related ideas organized per paragraph. | **Strictly one idea per sentence.** |
| **Visual Elements** | **No pictures or icons** (relies purely on clean layout and white space). | **Mandatory visual pairing** for every single line via `[Icon: {EMOJI} \| {Art Description}]`. |
| **Glossary Section** | Key terms bolded and defined in context or in a closing glossary. | Mandatory **"Words to Know"** section placed directly at the beginning of each part. |
| **Voice** | Active voice strongly preferred. | **Active voice strictly required.** |

---

## The System Prompts

### 1. Plain Language System Prompt
* **File / Target:** `plain_language_system_prompt.md`
* **When to use:** 
  * Factsheets, standard policy briefs, agency notices, and public guides.
  * When readers need simple syntax and common vocabulary, but find broken-out lines and heavy icon layouts distracting or hard to follow.
* **Key Mechanisms:**
  * Active voice enforcement.
  * Joins short sentences using conjunctions (*and*, *but*, *because*) to maintain natural reading flow.
  * Eliminates bureaucratic jargon while retaining all procedural and factual requirements.

### 2. Easy Read System Prompt
* **File / Target:** `easy_read_system_prompt.md`
* **When to use:**
  * Resources specifically tailored for individuals with IDD, self-advocacy groups, and visual learners.
  * When maximum accessibility and visual anchors are necessary.
* **Key Mechanisms:**
  * **One Idea Per Line:** Hard cap of one thought per line and 10–15 words per sentence.
  * **"Go Backwards to Move Forward":** Automatically introduces foundational background concepts before explaining advanced topics (e.g., explaining health insurance before defining Medicaid).
  * **Emoji + Icon Placeholders:** Emits `[Icon: 🗳️ | description]` tags preceding every sentence to serve as both an immediate visual aid and production spec for visual designers.
  * **ASAN House Rules:** Prohibits police/shields for "safety" (uses a neutral knight symbol instead) and prohibits icons on introductory list lead-in sentences.

---

## Implementation Guide (Gemini 3.8 Flash)

### Recommended Generation Parameters

```json
{
  "temperature": 0.2,
  "topP": 0.8,
  "presencePenalty": 0.0,
  "frequencyPenalty": 0.1
}
```
*A lower temperature (0.1 to 0.3) is recommended to ensure strict adherence to reading-level constraints, word count caps, and formatting schemas.*

### Example User Turn

To run a translation, pass the chosen system prompt in the system instruction field, then format the user message as follows:

```text
Please translate the following policy text into [Plain Language / Easy Read]:

"""
[Paste complex legal, policy, medical, or administrative text here]
"""
```

---

## Compliance & Editorial Checklist

When evaluating the model's output, verify these criteria:

- [ ] **No Content Loss:** Were any rules, dates, rights, or penalties cut? (If yes, prompt the model to expand).
- [ ] **No Figures of Speech:** Are idioms like *"on the same page"* or *"ballpark figure"* replaced with literal language?
- [ ] **Pronoun Check:** Are pronouns like *"this"* or *"they"* ambiguous? (Subjects should be explicitly stated).
- [ ] **Voice Check:** Are all passive sentences (*"Action was taken by..."*) rewritten into active sentences (*"The agency took action..."*)?
- [ ] **Layout (Easy Read Only):** Does each sentence exist on its own discrete line preceded by an `[Icon: ...]` block?
