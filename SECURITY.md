# Security

## Reporting a problem

Email moose@himoose.com with "Security" in the subject line, what you found and how to reproduce it. Please do not open a public issue for a security problem. We reply within three business days.

This repository holds only the open source skills and the dashboard template. The Hi, Moose service, Hi, Moose MCP and the desktop app are not in this repository; report problems with them to the same address. How Hi, Moose MCP handles sign-in and data is described at https://himoose.com/docs/integrations/hi-moose-mcp/security/.

## What the skills can do

- The skills only read. They call the Hi, Moose MCP read tools for stored AI search results and never start new checks, change settings or write to your site.
- The skills hold no keys or passwords. You connect Hi, Moose MCP in your own Claude or ChatGPT account and sign in there. Nothing in this repository asks for a key.
- Results stay in your own chat. The skills send nothing anywhere else.

## Answers are outside text

Stored answers, prompts and source links come from AI search engines and the web. Hi, Moose MCP marks them as data. The skills tell the assistant to treat them as data and never follow instructions found inside them.

The dashboard template writes every value as plain text and only links `http` and `https` addresses. If you change the template, keep it that way: never insert answer text as HTML.

## Your report is private data

A report or dashboard made with these skills shows your brand's results and your competitors. Share it on purpose. Do not publish a filled-in dashboard page to a public site unless you mean to.

## Supported versions

Only the latest version on the main branch gets security fixes.
