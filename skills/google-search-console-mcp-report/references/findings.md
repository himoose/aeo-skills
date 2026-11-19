# The findings

How to work out each finding from the rows. Every finding is a statement about the numbers. None of them is a cause.

## Which number moved

Clicks are impressions times CTR, and CTR mostly follows the rank. So for each dropped or risen row from step 3, compare the row with its `previous` and name what moved the same way as the clicks:

| What the row shows | Say |
|---|---|
| `seen` is `previous` | No longer shown |
| `seen` is `current` | New in this period |
| Impressions moved by 20% or more | Shown less often (or more often): {impressions} impressions, {previous impressions} before |
| CTR moved by a fifth of its earlier value or more, and position moved by 0.5 or more | Ranks lower (or higher): from {previous position} to {position} |
| CTR moved by a fifth of its earlier value or more, and position moved by less than 0.5 | Fewer (or more) clicks at the same rank: CTR {ctr}%, was {previous ctr}% |
| None of these | Small changes in several numbers |

When both impressions and CTR moved, give both phrases, the one with the larger percentage change first. Keep the cell to those phrases and their numbers. Only when the position moved by 0.5 or more against the clicks, add it in a few words ("although it ranks lower, from 1.0 to 6.1").

For the "at the same rank" rows, add one sentence under the table on what can be checked: what sits above the result for that search now (an AI answer, ads, a results box) and whether the page's title changed. Do not say which it is.

Leave a row out when its clicks changed by fewer than 10, unless nothing else is left. When `scan.complete` is false, a row marked `current` or `previous` may exist in the other period among rows that were not read: say "not among the rows read" in place of "no longer shown".

## On page one, not clicked

From the searches-with-pages pull in step 4:

- Keep rows with position up to 10.0 and at least 100 impressions. Leave out brand searches.
- Work out the middle CTR of those rows (the median), for scale.
- Of the rows at or below that middle CTR, report the five with the most impressions, each with its page, position, impressions, clicks and CTR. Give the middle CTR once, and how many rows it rests on. When the middle CTR is 0, say how many of the rows got no clicks instead.

What to say about them: people saw the result on the first page and did not click. What can be checked is whether the results page itself answers the search (an AI answer, a definition box, a results box) and whether the title matches what the searcher wants. Search Console does not say which. For these searches, being named and cited in the answer on the page counts as well as the click, so carry them into the AI search part.

## Just off page one

From the same pull:

- Keep rows with position above 10.0 and up to 20.0, and at least 10 impressions. Leave out brand searches.
- Leave out a search the page was clearly not written for.
- Group the rows by page. For each page keep its three searches with the most impressions.
- Report up to five pages, most impressions first: the page, the searches, and the position and impressions of each.

Next step for each: a refresh of the page aimed at its top search (`refresh_content`), offered.

## Two pages for the same search

From the same pull:

- Add up, for each search, the impressions of every page it appears with in the pull. Find searches with two or more pages where each page has at least 10 impressions and at least 10% of that sum.
- Leave out brand searches: Google often shows several pages of a site for its own name.
- Report up to five searches, largest sum first, each with its pages and the position, impressions and clicks of each page. A search with its pages is one entry of the table, however many rows it takes.

Next step: pick the page that should be the main one for that search, and link the other to it or fold it in. A link plan for the main page (`find_internal_links`) is offered.

## Questions people search

From the question pull in step 4:

- Drop rows that are not questions, such as a name that starts with a question word.
- Merge rows that ask the same question in different words ("what is a crm", "what is crm", "what is a crm tool") into one. Add up their impressions and clicks, and keep the wording and the position of the row with the most impressions.
- Take up to 15 merged questions, most impressions first.
- When `check_site_coverage` is available, call it once with those questions as `topics`. Each topic comes back with a `decision`; the crawl date is `crawlCompletedAt`.
- Look each question up in the searches-with-pages rows of step 4. When a page of the site already ranks for it there, a page exists, whatever the check says.

Then sort them:

| A page exists | Position | It is |
|---|---|---|
| No: the check says `uncovered` or `partial`, and no page ranks for it | any | A new piece. Name the closest page when the check gives one. Offer a brief (`create_content_brief`). |
| Yes: the check says `covered`, or a page ranks for it | worse than 10.0 | A refresh of that page (`refresh_content`), offered. |
| Yes | 10.0 or better | Answered and on page one. No to-do from this part. |
| The check says `unknown` and no page ranks for it | any | Say the check could not run for it and give the reason from the row. |

The question pull counts by property and the searches-with-pages pull counts by page, so the same search can show different impressions in the two. Use the question pull's numbers in this part.

The table in the report lists up to five questions whatever the result, those that need work first, then the rest by impressions. Give the date of the crawl the check used. Without `check_site_coverage`, list the questions with their numbers and say the site was not checked for pages that answer them.

## Pages that lost clicks over four weeks

From the lost-clicks call in step 4:

- Keep pages whose clicks fell by 20% or more and by at least 10 clicks against the 28 days before. Leave out pages that are not content, such as sign-in and account pages.
- Report up to five, with "Which number moved" for each.
- For the first two only (leave the search empty for the others), find the searches behind the loss: `search_console_query` on the 28 days with `dimensions: ["query"]`, `compare: true`, `sortBy: "clicksChange"`, `sortDirection: "asc"`, `rowLimit: 5` and a `page` filter with `equals` and the page address. Name the search that lost the most; it is the `targetQuery` when a refresh is offered. When no search in those rows lost 5 clicks or more, Google has left the searches behind the loss out as too rare: say so, write "not shown by Google" in the column, and leave `targetQuery` out of a refresh so Hi, Moose works out the page's main search itself.

A four-week change is steadier than a one-week one, so these come before one-week drops in the to-do list.

## Google Search next to AI search

1. Call `visibility_list_tracked`. Keep `project.ownedDomains`, the tracked prompts with their text, and `history`. When `history.answersStored` is 0, write the "not tracked yet" sentences from the layout and stop this part.
2. Call `visibility_get_summary` with `from` and `to` set to the 28 days, `sections: ["totals", "citations"]`, `citationsList: "pages"`, `citedDomains` set to the owned domains and `citationsLimit: 100`. Keep `totals.answers`, `promptCount`, and each page with its `answers` and `byEngine`.
3. Match those pages with the top pages from step 4 by address. Ignore `http` or `https`, a leading `www.`, a trailing slash, anything after `#` and anything after `?`.
4. Make three short lists, up to five pages each in the written report and up to ten in the dashboard. Leave out pages that are not content, such as sign-in, account, cart and legal pages.
   - **In Google and in AI answers:** top Google pages that the stored answers also cite. Give the Google clicks, the number of stored answers that cite the page, and the engines.
   - **In Google, not cited in the stored answers:** top Google pages no stored answer cited, most clicks first. An AEO audit of the page (`run_aeo_audit`) is offered only for a page whose subject one of the tracked prompts asks about, and for at most two. When the tracked prompts ask about other subjects than these pages, say so in one sentence and offer no audit: the stored answers cannot show how such a page does in AI search.
   - **Cited in AI answers, not among the top Google pages:** pages the stored answers cite that are not among the 50 top Google pages, most cited first. Give the number of stored answers and the engines. Do not give a Google click number for them: none was read.
5. Compare the searches in the report (the dropped ones and the ones on page one that nobody clicks) with the text of the tracked prompts yourself. Only when a tracked prompt asks the same thing as one of those searches, call `visibility_check_topic` with the search as `question` and `lookbackDays: 28`, for at most three searches. Report, per engine, whether the brand was named and cited. When no tracked prompt asks the same thing, say in one sentence that Hi, Moose has no stored AI answers for these searches. Do not turn the Google searches into a list of prompts to add.

Rules for this part:

- Name the two Google engines first when they are tracked (returned as "Google Search AI Overview" and "Google AI Mode"): they sit on Google's own results pages.
- A page that is "not cited in the stored answers" was not cited for the tracked prompts in this window. It may be cited for questions nobody tracks. Never write "not cited by AI".
- Give the window, `totals.answers` and `promptCount` once at the top of the part.
- Never set a change in Google clicks beside AI citations as cause and effect.
