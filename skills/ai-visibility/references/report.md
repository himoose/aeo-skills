# Written report

A short, honest report the user can read in five minutes or forward to their team.

**Window.** Default: the last 30 days, compared with the 30 days before. Use the user's dates or period if they gave one ("last week" = 7 days, "this month" = from the 1st to today).

## Steps

1. `visibility_list_tracked`.
   - Note the brand name, the engines and topics tracked, the competitors, the schedule and `history` (first and last day, answers stored).
   - If `history.answersStored` is 0, tell the user Hi, Moose has no stored results for this project yet and that they appear after the first visibility run in the Hi, Moose app. Stop.
   - If the window starts before `history.firstDay`, say so in the report, and drop the comparison when the earlier window has no answers.
2. `visibility_get_summary` with the window (`lookbackDays`, or `from` and `to`), `sections: ["totals", "engines", "topics"]` and `compare: true`.
3. `visibility_get_summary` again with the same window, `promptType: "non-branded"`, `sections: ["totals", "engines"]` and `compare: true`. Prompts that name the brand almost always get answers that mention it, so the overall mention rate can hide how the brand does when buyers ask without naming it. Report both. Skip this when `visibility_list_tracked` shows no non-branded prompts.
4. `visibility_get_summary` again with the same window and `sections: ["competitors"]`. Ask for competitors in its own call: this section can be large.
5. `visibility_list_results` with the same window, `engines: [<the engine with the lowest mention rate and at least 10 answers>]`, `mentioned: false`, `pageSize: 10`. These are examples of answers that left the brand out, with the competitors they named instead.
6. `visibility_get_answer` for at most two answers: one recent answer that left the brand out (from step 5) and one recent answer that mentioned or cited it (call `visibility_list_results` with `mentioned: true`, `pageSize: 3` to find one). Quote one or two sentences from each, never more.
7. `visibility_list_opportunities` with `limit: 5` for the next steps. It reads the last 7 days by default; say so. If `totalOpen` is higher, say how many more are open and offer the full to-do list.

## Rules for the report

- **Small samples.** Leave engines, topics or days with fewer than 10 answers out of rankings and comparisons. List them in one line under "About these numbers" with their answer counts.
- **Different totals.** Different numbers of runs or prompts between windows also change the totals; mention it when `totals.answers` differs by more than a quarter.
- **Compare like with like.** When an engine or prompt has answers in only one of the two windows, the totals are not comparable. Name the engines present in only one window, and also give the change for the engines present in both (add up their answers, mentions and citations from `byEngine` and `comparison.byEngine`).
- **Branded and non-branded.** Lead with the non-branded numbers when there are any: they show whether the brand comes up when buyers do not name it.
- **Share of answers.** In the competitors section, `sharePct` is the share of answers in the window that name that brand.
- You may drop "(local fetch)" from engine names in tables after explaining it once.

## Output

Write the report in markdown, using `references/report-template.md`. Keep it under about 600 words plus tables. Lead with the finding that matters most, in plain words. When something went down, show where (engine, topic, prompt) before anything else.

Offer one follow-up at the end: the interactive dashboard of the same numbers, the full text of a quoted answer, or the full to-do list.
