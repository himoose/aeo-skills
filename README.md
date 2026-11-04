# AEO skills for Claude and ChatGPT

Open source skills by [Hi, Moose](https://himoose.com) for answer engine optimization (AEO), also called generative engine optimization (GEO) or AI SEO: getting your brand mentioned and cited in the answers ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini and Grok give. Use them inside Claude, ChatGPT or your coding agent.

[![Hi, Moose AEO MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/com.himoose.mcp/hi-moose-aeo/badges/score.svg)](https://glama.ai/mcp/connectors/com.himoose.mcp/hi-moose-aeo)
[![M8ven Score](https://m8ven.ai/badge/mcp/himoose-aeo-skills-g3wntp?v=d16ac61fc1512215cb94cf52df9cecdb)](https://m8ven.ai/mcp/himoose-aeo-skills-g3wntp?s=readme)

| Skill | What it does |
|---|---|
| [`ai-visibility`](skills/ai-visibility/SKILL.md) | AI search visibility dashboard, report and to-do list from your Hi, Moose results. |
| [`publish-ready-draft`](skills/publish-ready-draft/SKILL.md) | One AI search opportunity or topic taken all the way to a finished article: researched brief, draft, AEO audit with the fixes applied, internal links, key points, FAQs and featured image. |

New skills are added often. Each one lives in its own folder under `skills/` and installs on its own.

## ai-visibility

See how AI engines talk about your brand: how often they mention and cite you, against which competitors, and what to fix.

![AI search visibility dashboard made by the ai-visibility skill](docs/dashboard.png)

### What you can ask for

| Ask | You get |
|---|---|
| "Build my AI search visibility dashboard." or "How are we doing in AI search?" | An interactive dashboard (the default): pick 7, 30 or 90 days or your own dates, compare with the period before, filter by AI engine, hover over any chart for the numbers, see your tracked brand against competitors and the answers that left you out, and work through your to-do list with "Open in Hi, Moose" buttons. Save charts as PNG, the numbers as CSV and the page as PDF. |
| "Write my AI search visibility report as text for an email." | A short written report: how often AI engines mention and cite your brand, what changed since the period before, results by engine and topic, competitors, quoted answers and next steps. |
| "What should I work on this week to show up more in AI search?" | Your open fixes, ranked: the top five in full with the prompts, engines and competitors behind them, the rest one line each. |

The skill only reads results Hi, Moose has already stored. It never runs new checks, changes settings or publishes anything.

## publish-ready-draft

One piece of content, from the gap in AI search to an article you can publish, in one ask.

A general AI assistant writes an article from a few web searches and what it already knows, so it tends to repeat what already ranks. This skill runs the piece through Hi, Moose step by step and edits between the steps:

1. **Brief.** Hi, Moose reads the live Google results, the top three ranking pages in full, People Also Ask, what Google AI Overview and ChatGPT answer right now, the searches Gemini runs, and your own site, documents and Brand Truth Profile. Started from an opportunity, it also reads the pages the AI engines cited where your brand was left out. The brief plans the piece around the gaps none of those pages cover.
2. **Draft.** Hi, Moose writes the first draft in your brand's voice from the brief.
3. **AEO audit, then the fixes.** Hi, Moose audits the draft for how well answer engines can read and cite it. The skill applies the audit's text fixes to the draft itself.
4. **Internal links.** Hi, Moose plans links both ways from the crawl of your site; the skill places the outgoing ones in the text and lists the incoming ones for you to add.
5. **Key points and FAQs.** Short quotable statements under the introduction, FAQs at the end, with the FAQPage schema ready to paste.
6. **Featured image.** A 1200 by 630 image in your saved image style, with alt text.

You get the article in full, the image, a publish checklist (incoming links to add, schema to paste, facts to verify, the technical items only the live page can fix) and the list of edits made.

### From your AI visibility to-do list

Content items in the `ai-visibility` dashboard have a **Copy brief request** button. Paste it and ask for the whole piece: the skill starts from that opportunity, so the brief knows which AI engines leave your brand out, which competitors they name instead, and which pages they cite, and reads those pages.

### What you can ask for

| Ask | You get |
|---|---|
| "Write me a publish-ready article from my top AI search opportunity." | The skill takes your top open content opportunity, tells you which one and whether it means a new article or a refresh of a page you have, and runs the whole piece. |
| A request copied from the dashboard's **Copy brief request** button, plus "and take it all the way to a draft" | The whole piece for that opportunity. |
| "Create a content brief for 'how to choose an SCA tool'." | Only the brief, in full, with the rest offered as the next step. |
| "Refresh our SCA guide at <URL> and get it ready to publish." | The refresh route: Hi, Moose compares the page with the current results and rewrites it keeping your structure and voice, then the audit, links, FAQs and image follow. |

Before a new piece, the skill checks whether your site already covers the topic. If a page already does, it refreshes that page instead of writing a second one.

### Plans

- **Free plan:** one run with the full live research a day (the brief). The other steps still run. Keep the Hi, Moose desktop app open while you ask.
- **Paid plans:** no daily limit, a choice of model, everything kept in your team's Library, live search evidence in audits and FAQs, and runs in the cloud when the desktop app is closed. See [pricing](https://himoose.com/pricing/).

## Quick start

1. **Get Hi, Moose (free).** [Download the desktop app](https://himoose.com/downloads/) and add your site. For `ai-visibility`, add the prompts you want to track and run your first visibility check.
2. **Connect Hi, Moose to your AI app.** Add a custom connector with the address `https://mcp.himoose.com/mcp` and sign in with your Hi, Moose account. [Step-by-step for Claude, ChatGPT and others](https://himoose.com/docs/integrations/hi-moose-mcp/).
3. **Add the skills** you want to your app: see [Install](#install) below.
4. **Ask** for your dashboard, your to-do list or a publish-ready article. Keep the Hi, Moose desktop app open while you ask.

## Install

### Claude.ai and the Claude desktop app

1. On this page, click **Code → Download ZIP**, and unzip the file.
2. Inside, open the `skills` folder and zip one skill folder on its own, for example **`publish-ready-draft`**.
   - **Windows:** right-click the folder → **Send to → Compressed (zipped) folder**.
   - **Mac:** right-click the folder → **Compress "publish-ready-draft"**.

   You now have `publish-ready-draft.zip` with the `publish-ready-draft` folder inside it.
3. In Claude, go to **Customize → Skills**, click **+**, then **Create skill → Upload a skill**, and choose the zip file.
4. Repeat steps 2 and 3 for each skill you want.
5. Make sure **code execution** is turned on in Claude's settings; skills need it.
6. Start a new chat, check that the Hi, Moose connector is turned on for it, and ask.

### Claude Code

This repository is also a Claude Code plugin. One install adds every skill and the Hi, Moose connector, and updating the plugin adds new skills as they come out:

```
/plugin marketplace add himoose/aeo-skills
/plugin install himoose@himoose
```

Then run `/mcp`, choose `plugin:himoose:himoose` and **Authenticate** to sign in. Ask in plain words, or run `/himoose:ai-visibility` or `/himoose:publish-ready-draft`.

If you already connected Hi, Moose to Claude Code yourself, you will see the same tools twice. Remove one of them in `/mcp`.

### ChatGPT

Skills are available on some ChatGPT plans only; OpenAI lists Business, Enterprise, Healthcare and Edu workspaces ([Skills in ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt)).

1. Connect Hi, Moose: **Settings → Apps → Add → Create custom MCP server**, address `https://mcp.himoose.com/mcp` ([details](https://himoose.com/docs/integrations/hi-moose-mcp/)).
2. Add each skill folder you want (for example `skills/publish-ready-draft`) as a skill, following OpenAI's instructions for your workspace.
3. Type `@` in a chat to pick the skill, or just ask.

### Codex and other agents

The skills use the open [Agent Skills](https://agentskills.io) format. Copy the skill folders you want from `skills/` into your agent's skills folder (in Codex you can also ask the built-in `$skill-installer` to install it from this repository; see [OpenAI: Build skills](https://learn.chatgpt.com/docs/build-skills)), and connect `https://mcp.himoose.com/mcp` as a remote MCP server with sign-in.

## Troubleshooting

| What you see | What to do |
|---|---|
| The assistant does not know the Hi, Moose tools | Connect Hi, Moose (Quick start step 2) and make sure the connector is turned on in this chat. Start a new chat after connecting. |
| "The Hi, Moose app is not open" or the request keeps waiting | Open the Hi, Moose desktop app on the computer that holds your results, signed in with the same account. |
| "No stored results yet" | Run a visibility check in the Hi, Moose app first. Results appear after the first run. |
| The dashboard's Export or Save PNG buttons do nothing | Some chat previews block downloads. Save the page as an HTML file, open it in your web browser and try again. |
| "Open in Hi, Moose" does nothing | Install or update the Hi, Moose desktop app, and allow your browser to open it when it asks. |
| Sentiment shows "not scored" | Sentiment, narrative and feature accuracy scores are part of paid plans. Mentions, citations, rank and competitors work on every plan. |
| "Free plans get one run with live search research a day" | The free plan's daily researched run is used. The brief was made without the live research; wait until tomorrow for a researched one, or move to a paid plan for no daily limit. |
| A step keeps saying it is still working | A brief or draft takes one to three minutes and an audit two to four; the whole article takes 10 to 15 minutes. On the free plan the steps run in the Hi, Moose desktop app, so keep the app open and signed in. |

## FAQ

**How do I track whether ChatGPT, Perplexity or Google AI Overviews mention my brand?**
Add the prompts your buyers ask to [Hi, Moose](https://himoose.com). It runs them on ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini and Grok on your schedule and records whether each answer mentions or cites your brand, and which competitors it names. The `ai-visibility` skill then shows those results in Claude or ChatGPT.

**Is there a free AEO or GEO tool I can use with Claude?**
Yes. The skill is free and open source (MIT), and Hi, Moose has a free plan with unlimited prompts on the engines above, run on your own computer. Paid plans add sentiment, narrative and feature accuracy scoring, cloud runs and cloud history.

**How do I build an AI search visibility dashboard?**
Install the skill, connect Hi, Moose, and ask "Build my AI search visibility dashboard." You get one HTML page with date and engine filters, charts, competitors and a to-do list. Open it in a browser, share it with your team, or use it as a starting point for a dashboard in your own app.

**How is this different from asking Claude or ChatGPT to write the article?**
A general assistant writes from a few web searches and what it already knows. Hi, Moose reads the top three ranking pages in full, People Also Ask, current AI answers, the searches Gemini runs, your brand documents and your own site, plans the piece around the gaps none of the ranking pages cover, writes it in your voice, audits it for answer engines, and the skill applies the fixes. Started from the AI visibility to-do list, it also knows which AI engines leave your brand out and reads the pages they cite instead.

**Can I make a researched article for free?**
Yes. The free Hi, Moose plan includes one run a day with the full live research. Paid plans remove the daily limit.

**What is AEO, GEO or AI SEO?**
Three names for the same work: answer engine optimization (AEO), generative engine optimization (GEO) and AI SEO all mean getting your brand mentioned and cited in AI answers, the way SEO aims for search results.

**Why not call the OpenAI or Perplexity API myself?**
You can, but API answers can differ from what people see in the apps, and you would still need to schedule checks, keep history, find your brand and competitors in each answer and track which pages get cited. Hi, Moose does that and the skill reads the results. See [Why Hi, Moose collects the data](#why-hi-moose-collects-the-data).

**Does it work in Claude Code, Codex or other coding agents?**
Yes. In Claude Code it installs as a plugin with the Hi, Moose connector. In Codex and other agents that read `SKILL.md` skill folders, copy the `skills/ai-visibility` folder and connect Hi, Moose MCP. See [Install](#install).

**Does the skill send my data anywhere?**
No. The skills work through Hi, Moose MCP and show the results in your own chat. `ai-visibility` only reads your stored results. `publish-ready-draft` makes a brief, a draft, an audit, FAQs, key points and an image, which Hi, Moose also saves in your Library; it publishes nothing. The skills hold no keys.

## Why Hi, Moose collects the data

You could call the ChatGPT and Perplexity APIs with a list of prompts and search the answers for your brand name. Hi, Moose does more than that:

- **Answers as people see them.** Hi, Moose reads ChatGPT, Perplexity, Google AI Overviews, Google AI Mode, Gemini and Grok in a browser on your own computer, so you get the answer a person sees, with its sources. Answers from the raw APIs can differ from what the apps show.
- **Scored answers.** Every answer is checked for brand mention, citation of your pages, rank, competitors named and pages cited.
- **History.** Checks run on your schedule (daily, weekdays, weekly or manual) and every answer is kept, so you can compare periods.
- **Free plan.** Unlimited prompts on all the engines above, run on your computer. Paid plans add sentiment, narrative and feature accuracy scoring, cloud runs and cloud history. See [pricing](https://himoose.com/pricing/).

## About the numbers

- Results cover only the prompts you track, on the engines you track.
- Every number comes with its period and how many answers it rests on. Engines or topics with fewer than 10 answers are marked as small samples.
- The skill reports what the engines answered on run days. It never claims why something changed.

## What's in this repository

```
skills/ai-visibility/
  SKILL.md                      what the skill does and which file to follow
  references/dashboard.md       how to build the dashboard
  references/report.md          how to write the report
  references/report-template.md the report layout
  references/weekly-actions.md  how to build the to-do list
  assets/dashboard.html         the dashboard page (opens with sample data)
  agents/openai.yaml            ChatGPT and Codex settings
skills/publish-ready-draft/
  SKILL.md                      the steps from opportunity or topic to a finished article
  references/apply-audit-fixes.md  how the audit's fixes are applied to the draft
  references/handoff.md         the layout of the finished package
  agents/openai.yaml            ChatGPT and Codex settings
.claude-plugin/                 Claude Code plugin and marketplace files
.mcp.json                       the Hi, Moose connector for Claude Code
```

Open `skills/ai-visibility/assets/dashboard.html` in your browser to try the dashboard with sample data.

## Security and privacy

The skill holds no keys and sends your data nowhere except your own chat. Answers from AI engines are treated as data, never as instructions. See [SECURITY.md](SECURITY.md).

## License

MIT, see [LICENSE](LICENSE). The skill and the dashboard template are open source. Hi, Moose and Hi, Moose MCP are a service by Farmball, LLC.
