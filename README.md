# find-similar-vertical-agent-founders

A [Sai](https://simular.ai) skill that builds a prospect list of founders and leaders at **vertical AI agent startups**: companies building an AI agent for one industry or workflow, where the agent has to operate websites, portals or business software for its users. These companies are likely buyers of computer-use capability, such as Simular's [Sai API](https://platform.simular.ai/documentation).

You give it one company (or a person at one). It finds similar companies on Google and LinkedIn, picks the right people at them, rates each one, and appends them to a Google Sheet.

The full instructions the agent follows are in [SKILL.md](SKILL.md).

## What it does

1. **Reads the input company.** It works out what the company does, who it sells to, and which software its agent has to operate, then reduces that to 3–5 short search phrases.
2. **Confirms with you.** One card shows the search phrases and asks for extra criteria (e.g. US only, Seed / Series A only) and how many people you want. Nothing is searched until you answer.
3. **Searches Google and LinkedIn for every phrase.** Both sources always run. Results are pooled and de-duplicated by LinkedIn URL.
4. **Rates each fit.** Importance is High, Medium or Low, with a short Reason that names the source (Google, LinkedIn or both). Companies that sell computer use or browser automation themselves are left out as competitors.
5. **Appends to the sheet.** New people go at the bottom, written by column name. Existing rows are never edited, moved or re-sorted.

LinkedIn use is read-only: no connecting, following, messaging or reacting.

## What it needs

- **Google Sheets access** to the target sheet (read the header and existing rows, append new rows). The default sheet is set in SKILL.md; change it to your own.
- **A signed-in LinkedIn session** in the browser, for LinkedIn people search and opening profiles. Opening a profile shows up in that person's "who viewed your profile" unless you browse in private mode.
- **Web search** (Google) and access to the YC company directory.

## How to run it

Ask Sai something like:

> Find founders similar to https://www.example.com and append them to the sheet.

The input can be a **company name, a company URL, or a LinkedIn profile URL**. Sai then shows a card with the proposed search phrases and target count. Keep, remove, edit or add phrases, pick a count, and it runs.

## Sheet columns

The skill reads the header row on every run and writes by column name, so the order can change and you can add your own columns.

| Column | What goes in it |
|---|---|
| Company Name | The candidate's company |
| Title | Their role (Founder, CEO, CTO, Head of Product…) |
| Full Name | The person's name |
| Sector | Short label, e.g. `AI insurance`, `AI healthcare RCM`, `AI IT ops` |
| What they build | One plain sentence on what the agent does and for whom |
| LinkedIn URL | Profile link, used to de-duplicate |
| Importance | `High`, `Medium` or `Low` |
| Reason | Source (Google / LinkedIn / both) plus why they fit and why that Importance |
| Reference Company | The company this search started from, so you can filter by search |

There is no Rank or Status column. If one exists in the sheet, the skill ignores it.

## Installing

Import this folder (or a zip of it) as a skill in Sai: **Settings → Skills → Import skill**. The skill's front matter in SKILL.md carries its name and description.

## License

[MIT](LICENSE)
