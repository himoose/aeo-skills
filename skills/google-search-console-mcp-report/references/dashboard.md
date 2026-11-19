# Interactive dashboard

Fill the template in `assets/dashboard.html` with what steps 1 to 5 found and hand the user one HTML page. The page draws the charts, does the period buttons, hover details and exports itself, with no outside scripts, fonts or images, so it works as a Claude artifact, in ChatGPT, or saved as a file and opened in a browser.

The page is a snapshot: it holds the numbers from the moment you build it. For newer numbers the user asks for a new dashboard.

## What the page shows

| Tab | Charts and lists | Follows |
|---|---|---|
| Overview | "In short", four number tiles, a line chart by day (clicks, impressions, CTR or position, with the period before as a dashed line), and a bar chart of clicks from brand and non-brand searches | The 7, 28 and 90 day buttons |
| What changed | A bar chart of the change in clicks for searches and one for pages, each with its table | The main window |
| Where to work | A dot chart of position against CTR, a bar chart of where impressions and clicks sit by position, and the five lists | The 28 days |
| Google and AI search | A bar chart of each page's Google clicks beside the stored AI answers that cite it | The 28 days |
| To-do list | The to-do items, each with a "Copy request" button | |

## Steps

1. Do steps 1 to 5 of `SKILL.md`, with the 180 days of daily numbers and the brand calls for all three periods that it lists for the dashboard.
2. Work out the to-do items as `references/report-layout.md` describes for "To do": at most five, four-week findings first.
3. Read `assets/dashboard.html`. Replace only the JSON inside `<script type="application/json" id="dashboard-data">` with the data block below. Change nothing else in the file.
4. Deliver the page:
   - Claude.ai or Claude Desktop: as an HTML artifact.
   - Claude Code, Codex or another coding tool: write it to `google-search-report-<project>-<today>.html` in the current folder and tell the user to open it in a browser.
   - ChatGPT: as an HTML file the user can download and open, or in canvas.

## The data block

Valid JSON, numbers as numbers, no rounding. Rows are short arrays to keep the page small.

```json
{
  "schemaVersion": 1,
  "sample": false,
  "brand": "<project.brandName, or the project name>",
  "property": "<property.displayName>",
  "generatedAt": "<today, YYYY-MM-DD>",
  "mainDays": 7,
  "daily": [["<day>", <clicks>, <impressions>, <position>]],
  "brandWindows": {
    "7":  { "brand": [<clicks>, <clicks in the 7 days before>], "other": [<clicks>, <clicks in the 7 days before>] },
    "28": { "brand": [0, 0], "other": [0, 0] },
    "90": { "brand": [0, 0], "other": [0, 0] }
  },
  "brandTerms": ["<each spelling counted as brand>"],
  "summary": ["<one sentence>", "<one sentence>"],
  "changed": {
    "from": "<main window start>", "to": "<main window end>", "beforeFrom": "<comparison start>", "beforeTo": "<comparison end>",
    "searches": [{ "name": "<query>", "clicks": 0, "before": 0, "moved": "<the one phrase from findings.md>", "brand": false }],
    "pages": [{ "name": "<page>", "clicks": 0, "before": 0, "moved": "<the one phrase from findings.md>" }],
    "note": "<the sentence on what can be checked for same-rank rows, or empty>"
  },
  "work": {
    "from": "<28-day start>", "to": "<28-day end>", "beforeFrom": "<28 days before, start>", "beforeTo": "<28 days before, end>",
    "rows": [["<query>", "<page>", <clicks>, <impressions>, <position>]],
    "questions": [{ "question": "<question>", "impressions": 0, "position": 0, "status": "none | partly | answered | unknown", "page": "<the page, or empty>" }],
    "crawlDate": "<date of the crawl the coverage check used, YYYY-MM-DD, or empty>",
    "lostPages": [{ "page": "<page>", "clicks": 0, "before": 0, "moved": "<the one phrase>", "search": "<search that lost the most, or 'not shown by Google'>" }]
  },
  "ai": {
    "tracked": true,
    "from": "<28-day start>", "to": "<28-day end>", "answers": <totals.answers>, "prompts": <promptCount>,
    "pages": [{ "page": "<page>", "clicks": <Google clicks, or null>, "answers": <stored answers that cite it, or 0>, "engines": ["<engine>"] }],
    "note": "<the per-engine lines for a checked search, or the one sentence that no tracked prompt asks the same thing>"
  },
  "todo": [{ "title": "<the exact issue in one sentence, with the page or search and its numbers and dates>", "next": "<the step>", "takes": "<what the Hi, Moose step takes>", "ask": "<request to paste into the assistant>" }],
  "notes": ["<one short line each>"]
}
```

Rules for the block:

- `mainDays`: 7 for the weekly report, 28 for a monthly one or a small property, 90 when the 28 days have fewer than 50 clicks. It sets which period button is on when the page opens.
- `daily`: every row of the property's daily call, oldest first: `[day, clicks, impressions, position]`. The page works out every total, CTR and comparison from these rows, so copy them exactly.
- `brandWindows`: for each period, the clicks of the brand call and of the non-brand call, each as `[this period, the period before]`, from `totals.clicks` and `compareTotals.clicks`. Leave a period out when its calls were not made.
- `summary`: two or three sentences for "In short", following the rules of `SKILL.md`: each names its dates, a one-week change is set beside the 28 days, and none claims a cause. When the device and country check ran, its sentence goes here too.
- `changed.searches`, `changed.pages`: up to five that dropped and five that rose, each with the `moved` phrase from "Which number moved". Set `brand` to true on brand searches.
- `work.rows`: every row of the searches-with-pages pull, each with its search and its page address written out. The page works out "On page one, not clicked", "Just off page one" and "Two pages for the same search" from these rows with the rules of `references/findings.md`, and marks brand searches from `brandTerms`. Use the same rules when you write the to-do items, so the page and the to-do list agree. The page cannot tell when a search is one the page was not written for; it lists such a row, and you leave it out of the to-do items.
- `work.questions`: up to five, those that need work first. `status` is `none` when no page answers it, `partly` when the check says `partial` and no page ranks for it, `answered` when a page exists, and `unknown` when the check could not run or was not available.
- `work.lostPages[].search`: filled for the first two pages only; an empty text for the others.
- `ai.pages`: up to ten pages for each of the three lists. A page in Google and in AI answers has both numbers. A page not cited in the stored answers has `answers` 0. A page that is not among the top Google pages has `clicks` null. When AI search is not tracked yet, set `"ai": { "tracked": false }`; the page then shows the two sentences for that case.
- `todo[].ask`: one sentence the user can paste into their assistant to start that step through Hi, Moose MCP, naming the page or search: `Use Hi, Moose to refresh the page https://example.com/guide/ for the search "best crm for small teams"`, `Use Hi, Moose to create a content brief for "what is a crm"`, `Use Hi, Moose to run an AEO audit of https://example.com/pricing/`, `Use Hi, Moose to plan internal links for https://example.com/guide/`. For two pages that compete, name both in `next` and let the user pick the main one; use the page with more clicks in `ask`. `takes` is one sentence, such as "A refresh in Hi, Moose takes three to six minutes."
- Page addresses: paths (`/pricing/`) when the page is on the property's main host, full addresses for any other host. In `ask`, always the full address.
- `notes`: always include "Google leaves rare searches out of the search rows, so the rows add up to less than the totals.", "Days are final about three days after they end; this page holds final days only." and "The page shows what changed, not why." Add the notes from the results that limit what the rows show, and "AI search numbers cover the tracked prompts on the tracked engines only." when the AI part is filled.

The template writes every value as text, never as HTML. Keep it that way and do not add values anywhere except the data block.

## After the page

In three to five sentences, give the main findings with their dates: the clicks and the change for the main window beside the 28 days, which number moved, the largest drop and rise, and the top to-do item. Mention that the period buttons and hover details work in the page and that the Export and Save PNG buttons work when the file is opened in a web browser. Then offer the to-do items by number, with what each takes and that each is a run on the user's Hi, Moose plan, and the written report for an email or doc.
