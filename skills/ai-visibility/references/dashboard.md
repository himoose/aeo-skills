# Interactive dashboard

Fill the template in `assets/dashboard.html` with the brand's stored Hi, Moose results for the last 90 days and hand the user one HTML page. The page does all filtering, hover details and exports itself, with no outside scripts, fonts or images, so it works as a Claude artifact, in ChatGPT, or saved as a file and opened in a browser.

The page is a snapshot: it holds the last 90 days at the moment you build it. For other dates the user asks for a new dashboard.

## Steps

1. `visibility_list_tracked`. Keep the project's `projectId` from `list_projects`. Take `project.brandName` and `history`. If `history.answersStored` is 0, tell the user there are no stored results yet (they appear after the first visibility run in the Hi, Moose app) and stop. Note whether any prompt has `promptType: "non-branded"`.
2. `visibility_get_summary` with `lookbackDays: 90` and `sections: ["trend"]`. Use `trendByEngine`.
3. If there are non-branded prompts: `visibility_get_summary` with `lookbackDays: 90`, `promptType: "non-branded"` and `sections: ["trend"]`. Use `trendByEngine`.
4. For each of 7, 30 and 90 days: `visibility_get_summary` with that `lookbackDays` and `sections: ["topics", "competitors"]`. Use `range`, `totals.answers`, `byTopic` and `competitors` (`ownBrand` and `rows`). The competitors part can be large; copy only what the data block needs.
5. `visibility_list_results` with `lookbackDays: 90`, `mentioned: false`, `pageSize: 200`. Skip rows where `available` is `false`.
6. `visibility_list_opportunities` with `limit: 25`.
7. Read `assets/dashboard.html`. Replace only the JSON inside `<script type="application/json" id="dashboard-data">` with the data block below. Change nothing else in the file.
8. Deliver the page:
   - Claude.ai or Claude Desktop: as an HTML artifact.
   - Claude Code, Codex or another coding tool: write it to `ai-visibility-dashboard-<project>-<today>.html` in the current folder and tell the user to open it in a browser.
   - ChatGPT: as an HTML file the user can download and open, or in canvas.

## The data block

Valid JSON, numbers as numbers, no rounding. Lists of rows are short arrays to keep the page small.

```json
{
  "schemaVersion": 2,
  "sample": false,
  "brand": "<project.brandName>",
  "projectId": "<projectId from list_projects>",
  "generatedAt": "<today, YYYY-MM-DD>",
  "span": { "from": "<range.from of the 90-day call in step 2>", "to": "<its range.to>" },
  "engines": ["<engine name>", "..."],
  "byEngine": [["<day>", <engine index>, <answers>, <mentioned>, <cited>]],
  "nonBranded": [["<day>", <engine index>, <answers>, <mentioned>, <cited>]],
  "windows": {
    "7":  { "from": "<range.from>", "to": "<range.to>",
            "topics": [{ "name": "<byTopic[].topic>", "answers": 0, "mentioned": 0, "cited": 0 }],
            "competitors": { "answers": <totals.answers>,
                             "rows": [{ "name": "<ownBrand.name>", "own": true, "mentioned": <ownBrand.mentioned> },
                                      { "name": "<rows[].name>", "own": false, "mentioned": <rows[].mentioned> }] } },
    "30": { "...": "same shape" },
    "90": { "...": "same shape" }
  },
  "prompts": ["<prompt text>", "..."],
  "names": ["<competitor name>", "..."],
  "missed": [["<date>", <engine index>, <prompt index>, [<name index>, "..."]]],
  "todo": {
    "from": "<range.from>", "to": "<range.to>", "totalOpen": <totalOpen>,
    "summary": "<one or two sentences when several items share one cause, else empty>",
    "items": [{ "id": "<opportunityId>", "appAction": "<appAction>", "ask": "<request to paste into the assistant, or empty>", "title": "<one plain sentence>", "priority": "<priority>", "effort": "<effortLabel>", "action": "<actionLabel>",
                "why": "<confidenceLine>", "next": "<next>", "engines": ["<engines>"], "prompts": <promptCount> }]
  },
  "notes": ["<one short line each>"]
}
```

Rules for the block:

- `engines`: every engine name in `trendByEngine` from step 2, most answers first, exactly as returned. `byEngine` and `nonBranded` use these positions; add an engine at the end if step 3 has one not in the list.
- `byEngine`, `nonBranded`: one row per `trendByEngine` entry with `answers` above 0: `[day, engine index, answers, mentioned, cited]`.
- `windows`: keys `"7"`, `"30"`, `"90"`. Up to 9 competitor rows after the brand, by `mentioned`.
- `missed`: up to 200 rows from step 5, newest first. `prompts` and `names` hold each prompt text and competitor name once; rows point to them by position. A row with no competitors named has `[]`.
- `projectId`: the id from `list_projects` for this project. The page uses it with each item's `id` to build "Open in Hi, Moose" buttons that open the item in the Hi, Moose desktop app; without it the buttons do not show. Never build the links yourself.
- `ask`: when the row has a `connectorTool`, one sentence the user can paste into their assistant to start that work through Hi, Moose MCP, naming the prompt or page from the row, for example `Use Hi, Moose to create a content brief for the prompt "best AEO tools for agencies"`, or for `visibility_get_answer`, `Use Hi, Moose to show me the evidence and the answers behind the opportunity <opportunityId>`. Leave it empty when there is no `connectorTool`.
- `todo.items`: every row from step 6, in order. The row `headline` is often cut off with "…"; write `title` as one plain full sentence from the headline. When several items share a cause (most often claims flagged as "not in the Brand Truth Profile" that may be true), say so in `summary` without calling any claim true or false.
- `notes`: always include "Counts cover the tracked prompts on the tracked engines only, not the whole of AI search." Add "Local fetch means Hi, Moose read the answer in a browser on the user's computer." when engine names end in "(local fetch)". Add one line naming engines that appear only in part of the 90 days, and one if the 90 days start before `history.firstDay`.

The template writes every value as text, never as HTML. Keep it that way and do not add values anywhere except the data block.

## After the page

In three to five sentences, give the main findings for the last 30 days with their sample sizes: the mention and citation rates and their change, the weakest engine, the competitor named most often, and the top to-do item. Mention that the period buttons, engine filter and hover details work in the page, that the Export and Save PNG buttons work when the file is opened in a web browser, and that topics and competitors follow the 7, 30 and 90 day buttons. Offer the written text report (for an email or doc) as a follow-up.
