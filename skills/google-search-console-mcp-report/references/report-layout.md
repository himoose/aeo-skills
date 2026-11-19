# The report

What the user gets, in this order and with these headings. Write it as markdown in the chat. The tables carry the numbers, so keep the sentences few: about 400 words outside the tables. Where the chat can make a page, a document or a spreadsheet of the rows, offer one after the report; do not make one unless asked.

Lead with the finding that matters most, in plain words. When something went down, show where (which searches, which pages) before anything else.

```markdown
# Google Search report: {property.displayName}

{start} to {end}, compared with {compare start} to {compare end}. Web search, final Search Console data.

## In short

{Three short sentences at most: clicks and the change, which number moved, and where the change comes from.}

| | Clicks | Impressions | CTR | Average position |
|---|---|---|---|---|
| Last 7 days | {clicks} ({change}) | {impressions} ({change}) | {ctr}% ({change} points) | {position} (was {before}) |
| Last 28 days | {clicks} ({change}) | {impressions} ({change}) | {ctr}% ({change} points) | {position} (was {before}) |

{One sentence on the daily trend: spread over the week, or on which days.}
{When the device and country check ran: one sentence on where the change sits.}

## Brand and non-brand searches

{The window's dates.}

| | Clicks | Before | Impressions | Before |
|---|---|---|---|---|
| Searches that name {brand} | {clicks} | {before} | {impressions} | {before} |
| All other searches | {clicks} | {before} | {impressions} | {before} |

Counted as brand: {terms}. Google leaves rare searches out of both rows, so they add up to less than the total above.

## What dropped

{The window's dates.}

| Search | Clicks | Before | Which number moved |
|---|---|---|---|
| {query} | {clicks} | {before} | {the phrase from findings.md} |

| Page | Clicks | Before | Which number moved |
|---|---|---|---|
| {page} | {clicks} | {before} | {the phrase from findings.md} |

{When a row is "fewer clicks at the same rank": one sentence on what can be checked.}

## What rose

{The same two tables.}

## Where to work

From the last 28 days, {start} to {end}.

### On page one, not clicked

| Search | Page | Position | Impressions | Clicks | CTR |
|---|---|---|---|---|---|

{One sentence: the middle CTR of the {n} searches on page one with 100 or more impressions, and what can be checked.}

### Just off page one

| Page | Searches | Position | Impressions |
|---|---|---|---|

### Two pages for the same search

| Search | Page | Position | Impressions | Clicks |
|---|---|---|---|---|

### Questions people search

| Question | Impressions | Position | On the site |
|---|---|---|---|
| {question} | {impressions} | {position} | {No page answers it / Partly: {page} / {page} answers it} |

### Pages that lost clicks over four weeks

| Page | Clicks | Before | Which number moved | Search that lost the most |
|---|---|---|---|---|

## Google Search next to AI search

From {answers} stored AI answers to {promptCount} tracked prompts, {from} to {to}. These cover the prompts {brand} tracks in Hi, Moose, not the whole of AI search.

**In Google and in AI answers**
- {page}: {clicks} Google clicks; cited in {n} stored answers ({engines}).

**In Google, not cited in the stored answers**
- {page}: {clicks} Google clicks.

**Cited in AI answers, not among the top Google pages**
- {page}: cited in {n} stored answers ({engines}).

{For each search checked with visibility_check_topic: one line per engine, named and cited or not. Or the one sentence that no tracked prompt asks the same thing.}

## To do

1. **{The exact issue in one sentence, with the page or search and its numbers.}**
   Next: {the step}. {The Hi, Moose step that starts it and what it takes.}
2. ...

## About these numbers

- Google Search numbers for {property}, web search, {dates}. Days are final about three days after they end.
- Google leaves rare searches out of the search rows, so the rows add up to less than the totals.
- {Any note from the results that limits what the rows show.}
- AI search numbers cover the tracked prompts on the tracked engines only.
- The report shows what changed, not why.

Google Search Console & AI search data, through [Hi, Moose AEO](https://himoose.com/?utm_source=skills-gsc-mcp-report).
```

## When AI search is not tracked yet

In place of the three lists, write these two sentences and nothing more:

"Search Console does not show which searches got an AI answer or which of your pages the AI engines cite. Hi, Moose records that for the prompts you track; add prompts on the Visibility screen in the Hi, Moose app and this part fills in after the first run."

## Rules for the report

- Leave out a part that has nothing in it, and say which parts were left out, and why, in "About these numbers".
- At most five entries in each table. Say in a few words when there were more.
- The to-do list has at most five items, at most two of one kind, taken in this order: pages that lost clicks over four weeks (most clicks lost first), searches on page one that nobody clicks (most impressions first), searches just off page one, questions no page answers, two pages for the same search, one-week drops, and last an AEO audit. Each item starts with the exact issue and has a "Next:" line. Say once, under the list, that each Hi, Moose step is a run on the user's plan and is made only when they ask.
- Write page addresses as paths (`/pricing/`) when the page is on the property's main host, and as full addresses for any other host. Say so once at the top.
- End with one line of offers: the same report for another window or against a year ago, the rows as a spreadsheet, or any to-do item by its number.
