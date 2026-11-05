# The plan

What the user gets, in this order and with these headings. Everything is markdown in the chat. The plan has no briefs in it; the "Brief" sections are added only after the user asks for briefs, and may be markdown files where the chat can make files. Where the chat can also make a document or page, offer it after the plan; do not make one unless asked.

```
## Content plan for the week of <Monday's date>: <project>

From <totalOpen> open AI search opportunities (<window from> to <window to>, <answersRead> stored answers, <promptCount> prompts, <engineCount> AI engines). <n> are writing work: <n> new pieces and <n> refreshes.

### This week

1. **<working title: the main prompt, or the brief's title once it exists>**
   <New piece | Refresh of <page URL>> · <topic> · <priorityLabel> priority · <effortLabel>
   Why: <prompts>, where <engines> leave <brand> out and name <rival> instead (<rivalPct>% against <youPct>% of <n> answers). Cited instead: <up to three page URLs>.
   <For a refresh: how the brand's page shows up now, from ownPages.>
   <One line for any change made in steps 4 to 6: "Merged with <other row>", "Your page <URL> already covers this, so this is a refresh", "Brief already saved on <date>".>
   Brief: <"<brief title>", saved <date> | none yet>

2. ...

3. ...

### Later, by topic

**<Topic>**
4. <New piece | Refresh of <URL>>: <headline as a plain sentence>. Next: <next>. (<effortLabel>, <priorityLabel> priority)
5. ...

**<Topic>**
6. ...

<For held-back rows: "Held back: Hi, Moose marks this as needing a check before work starts.">

### Not in this plan

<n> open items are not writing work: <n> to earn a place on pages the AI engines cite, <n> answers that describe <brand> wrongly, <n> changes to look into<, <n> leads to hold>. The AI visibility to-do list covers them.

### Next

- Briefs for this week's pieces: say "make the briefs", or name one ("brief number 1"). A new piece takes one to three minutes and a refresh three to six, and each is a full research run on your Hi, Moose plan.
- A brief for any later item: say "brief number 6".
- Take any piece to a publish-ready draft: say "write number 1".
```

## After the user asks for briefs

Add one section per brief, in plan order, as each finishes:

```
## Brief 1: <title>

<the brief in full, exactly as returned; for a refresh, the change list, the refresh brief and the revised draft in full>

<Free plan note, in the tool's own words, when a tool returned one.>
```

End with one line: the briefs are saved in the Hi, Moose Library, and "write number 1" takes a piece to a publish-ready draft.

## Rules for the plan

- Number every piece in one list, this week first, so the user can name any of them by number.
- In "Later", list topics in the order their highest piece sits in the queue, and pieces inside a topic in queue order. Give every open writing row its line; when there are more than 25 open items in all, say how many more are open and that they are in the Opportunities tab in Hi, Moose.
- Leave out a part that has nothing in it, except "This week".
- "Write number 1" uses the `publish-ready-draft` skill when it is installed, starting from that piece's brief. Without it, offer `create_draft` with the `briefId`.
- When a brief the user asked for failed or was not made, say so in its place in one line and carry on. Do not drop the piece silently.
