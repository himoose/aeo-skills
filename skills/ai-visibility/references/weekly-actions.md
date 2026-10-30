# To-do list

A ranked list of concrete fixes from Hi, Moose's Opportunities work queue, with the evidence behind each one.

## Steps

1. `visibility_list_opportunities` with `limit: 25` (the most the tool returns). The default window is the last 7 days compared with the 7 before, the same as the Opportunities tab in Hi, Moose. Use `lookbackDays` (up to 90) only if the user asks for a longer period. If the user asks for a set number of items, use that number instead, up to 25.
2. If `rows` is empty, tell the user there are no open items for this window, give `answersRead` and the window, and offer a longer window. Stop.
3. Keep every open row, in the order returned (already ranked by priority). Skip rows whose `status` shows the team marked them done, dismissed or snoozed.
4. For the top 5, call `visibility_list_opportunities` again with `opportunityId` to get the evidence: the prompts and engines with their state, competitors, pages cited instead, and what changed.
5. Write the list: the top 5 in full (see below), then every other open item as one line each. If `totalOpen` is more than 25, say how many more are open and that they are in the Opportunities tab in Hi, Moose.

## Writing each item

Before the list, look for items that share one cause and say so in one or two sentences at the top. The most common case: several "correct the description" items flag claims as "not in the Brand Truth Profile" when the claims may be true and the profile is simply missing them. Then the first step is to check those claims and add the true ones to the profile, which can clear several items at once. Name the claims; never say whether a claim is true unless the user or the evidence confirms it.

For each of the top 5, in this order:

- **Headline:** one plain sentence saying what the answers get wrong or where the brand is missing. The row's `headline` is often cut off with "…"; use the evidence (`detail.found`, `detail.flags[].reason`) to write the full sentence.
- **Why it matters:** one or two sentences from the evidence: which prompts, which engines, which competitors appear instead (`competitors`, `rivalName`, `rivalPct` against `youPct`), which pages get cited instead (`pagesCitedInstead`). Use numbers with their sample: "named in 1 of 8 answers".
- **Next step:** the row's `next`.
- **How to start:** if `connectorTool` is set, offer to run that Hi, Moose tool now (for example `create_content_brief`, `refresh_content`, `run_aeo_audit`, `find_internal_links`) and name what you would pass it (the prompt, the page URL). Otherwise use `connectorHint` or `appAction`, which point to the step in the Hi, Moose app.
- **Effort and priority:** `effortLabel` and `priorityLabel`, plus `confidenceLine` when present.

For every other open item, one line: the headline as a plain sentence, then `next`, then effort and priority in brackets. Number all items in one list so the user can say "do number 7".

After the list, add one line with the window, `answersRead`, `promptCount`, `engineCount` and `totalOpen` (how many open items exist in all).

## Rules for the list

- Full detail for the top 5 only, so the list stays readable; every other open item still gets its line.
- Never promise an outcome ("this will get you cited"). Say what the evidence shows and what the step changes.
- Do not run any Hi, Moose tool that creates content until the user says yes.
- Offer the interactive dashboard at the end: it holds the same list with "Open in Hi, Moose" buttons for each item.
