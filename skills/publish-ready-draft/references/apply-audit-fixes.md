# Applying the audit's fixes to the draft

The AEO audit returns two lists in its structured result: `recommendations` and `issues`. This file says how to turn them into edits on the draft markdown. The edits are yours; no tool makes them.

## What the audit gives you

Each recommendation has:

- `title`, `priority` (high, medium, low), `categories`
- `description` and `whyThisMatters`
- `currentText`: the passage in the draft it is about, when there is one
- `proposedText`: the copy to use, when the audit wrote some
- `editIntent`: `replace` (the proposed text takes the place of the current text) or `insert` (the proposed text is a new block that goes alongside)

Each issue has `title`, `category`, `severity`, `priority`, `description` and `implementation` (what to do about it, in words).

## Order

1. Recommendations with `proposedText`, high priority first, then medium, then low.
2. Issues with an `implementation` you can carry out in the text.
3. Everything else goes to the publish checklist.

## Replace

When `editIntent` is `replace` and `currentText` appears in the draft: put `proposedText` in its place. If `currentText` is not in the draft word for word, find the passage it clearly refers to (same topic, same shape: paragraph for paragraph, list item for list item) and replace that. If you cannot find it, treat the recommendation as an insert.

## Insert

When `editIntent` is `insert`, or the current text cannot be found: place `proposedText` where its topic sits in the section plan. A new definition goes right after the heading of the section that introduces the term. A new FAQ-style answer goes under the section that covers that question, not in the FAQ section at the end (the FAQ tool adds that later). A date or freshness line goes under the title. A list goes where the prose it summarises ends. Never append everything at the bottom.

## Proposed text is not evidence

The audit writes its proposed text to fix a weakness, and it sometimes fixes a "trust signals" weakness by asserting things nobody checked: "we tested each tool hands-on", "based on customer interviews", an author name, a review date, a price, an outside source. Before placing proposed text, read it sentence by sentence. A sentence that states something the draft and the brief do not contain stays out of the article and goes on the publish checklist under facts to verify, with the sentence quoted so the user can confirm it and paste it in. The rest of the proposed text goes in.

When a replacement drops a link the old passage carried, put the link back on the matching phrase in the new text.

## Keep the voice

The proposed text was written for this brand, but it was written in isolation. After placing it, read the paragraph before and after and smooth the joins: fix a repeated sentence, a changed tense, a term the draft spells differently. Do not expand the proposed text with your own material.

## Issues you can fix in the text

Typical ones, and what to do:

- **No direct answer near the top.** Move or write a two or three sentence answer to the target query under the introduction, using only what the draft already says.
- **Heading does not match the question people ask.** Reword the heading to the question or the plain phrase, keeping the section.
- **Long paragraphs, buried lists.** Split paragraphs at the idea breaks; turn a run of "first, second, third" prose into a list.
- **Vague claims.** When the draft states something without the number or the source that appears elsewhere in the draft or the brief, bring that number or source in. When nothing in the draft or brief supports it, soften the claim. Never invent support.
- **Missing definition of the main term.** Add one sentence of definition from the brief, where the term first appears.
- **Weak ending.** Close with what the reader should do next, drawn from the piece.

## Items that go to the checklist, not the draft

- Schema markup other than FAQPage (Article, HowTo, Organization), page dates, canonical tags, meta description and title tag, image alt attributes on existing images
- AI crawler access and robots rules
- Anything that needs the live page, the CMS or the site template
- Anything the audit flagged where the fix needs a fact the draft and brief do not contain: name the fact the user has to supply

## What you keep for the handoff

For every edit, one line: the recommendation or issue title, and what you did ("replaced the opening paragraph with the audit's direct answer", "added a definition of software factory under the first heading", "split the deployment section into a four-item list"). These lines go into the "What changed" part of the package.
