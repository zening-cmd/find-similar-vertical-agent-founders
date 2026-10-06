---
name: find-similar-vertical-agent-founders
description: Prospect founders and leaders at AI agent startups similar to a given company or person, as potential customers for Simular's Sai API (computer use). Input is a company name, company URL, or LinkedIn profile. The skill works out the selected company's characteristics and boils them down to 3–5 short search phrases, which it confirms with the user along with any other criteria and how many people they want. For every confirmed phrase it always runs both a Google search and a LinkedIn people search, pools the results, removes duplicates by LinkedIn URL, and picks up to the target from the combined pool. Finally, it rates each fit's Importance (High/Medium/Low), notes the source (Google, LinkedIn or both) in Reason, and appends new people to the bottom of the user's existing prospect Google Sheet, writing by column name and never re-sorting. Use when the user asks to "find similar founders/companies/profiles", "find more like X", build or extend a prospect list of AI agent builders, or add people to the vertical agent founders sheet.
---

# Find Similar Vertical-Agent Founders → Google Sheet

Builds and extends a prospect list of people at **vertical AI agent startups**. These are companies building an AI agent for one industry or workflow, where the agent has to operate websites, portals or business software for the user. They are likely buyers of computer-use (CUA) capability. They rarely say "computer use" publicly, because their customers don't need to know how it works, so judge the work the agent does, not the words on the profile.

**Why we're prospecting:** these people are potential customers for **Simular's Sai API** (https://platform.simular.ai/documentation). Their code hands a task to Sai, a computer-use agent working on a real Windows or macOS computer, and gets the result back. Sai uses apps and websites the way a person does, so it handles work where there is no API, or where the API doesn't cover the task:

- vendor portals and admin consoles
- legacy web apps and web apps behind a login
- forms with no import
- desktop software

It can also save a repeated workflow as replayable code. The best prospects are agent companies whose product has to get work done inside software like that and that would rather buy this capability than build it.

## The company preference (who counts)

**The ideal customer archetype.** This is the user's best example of a Sai API customer:

- An agent company serving the same **prosumers** Simular targets (individual professionals and small teams), but **much more deeply vertical**.
- Its product has to operate websites or apps for those users.
- It **can't build computer-use capability in-house**.

The proof case: a PR outreach agent builder and an ecommerce agent builder both said they already use computer use, and that their current third-party providers don't work well. Those are the companies most ready to switch to the Sai API.

- **When the selected company fits this archetype** (a vertical agent for prosumers or small businesses that needs to drive other software), carry the archetype into the fit profile as a must-have and give preference to candidates that match it.
- **Signals to look for**, since none of them will say "we need computer use":
  - a small team with no infrastructure or browser-automation engineers
  - product copy like "works with any website or portal", "no integration needed", "we do it for you"
  - job posts mentioning Playwright, Selenium, Puppeteer or browser automation
  - founders posting about flaky browser agents, scraping or automation tools
  - being named on a computer-use or browser-automation vendor's customer page
  - users who live in many outside tools (outreach, marketplaces, seller dashboards, portals)
- **Whatever company is selected,** archetype matches get higher Importance than otherwise-similar candidates, and their Reason says so (e.g. "Archetype match: prosumer-facing PR agent that has to work across media sites, small team, no in-house CUA.").

**Fit is relative to the selected company, not a fixed checklist.** Every search starts from the company (or person) the user selected:

- Work out its characteristics (step 1).
- Turn them into a **fit profile**.
- Confirm that profile with the user before searching (step 2).

After that, judge every candidate by how closely they match the confirmed fit profile. Only the rules below are fixed.

- **The one hard rule:** leave out companies that **sell** computer use, browser automation or browser-agent infrastructure themselves. They compete with the Sai API, so they're not prospects. Do not add them to the sheet.
- **The strongest preference:** the agent has to **do things inside websites or apps the company doesn't own**, on its users' behalf (portals, logged-in web apps, admin consoles, desktop software, forms). That's exactly what the Sai API is for, so give these people higher Importance. A similar company whose agent mostly talks, analyses or advises is still a candidate, just lower Importance. If the profile simply doesn't say how the agent works, keep them with Medium or Low Importance and say so in Reason rather than dropping them. That's expected, since these companies rarely mention it.
- **Size follows the selected company.** Prefer candidates of a similar size and stage. If the selected company is a seed startup, look for small startups. If it's larger or later-stage, a company doesn't need to be small to fit.
- **Everything else is similarity,** not a hard no: vertical, workflow, customer type, business model, product shape, geography. A candidate that differs on one of these can still fit if it matches well on the rest. Explain the trade-off in Reason.

Illustrations of work that happens inside other people's software (examples only, not a filter):
  - finance agents that navigate banking sites or log into ERPs such as NetSuite
  - insurance agents that submit forms to carrier portals or agency management systems
  - healthcare revenue-cycle, prior-auth or eligibility agents working in payer portals and EHRs
  - legal agents processing PDFs and filing on court or government portals
  - immigration filing, freight and customs, ecommerce operations (Shopify, Amazon Seller Central), PR outreach, procurement, ServiceNow or IT ops
**Not a fit** means a candidate that sells computer use, or one clearly unlike the confirmed fit profile (for example, a different kind of business altogether, or not building a product). Do not write them to the sheet; keep them only in the run's `tmp/` progress file so they aren't re-checked within the run.

Reference profiles the user liked: Eddie Guo (Echelon AI, agents for ServiceNow work), Elvis Sun (ex-Google, open-source PR agent tools), Nemo Feng (product lead at ZooWork, managed agents).

## Person preference (who to prioritise at a company)

Senior decision-makers first: **Founder / Co-founder / CEO > CTO > VP Engineering / Head of Engineering / Head of Product > Engineering Lead / early product lead.** Skip ICs, sales, recruiters and investors unless they are a founder.

## Inputs

- `target`: a company name, company URL, or LinkedIn profile URL. Required.
- `targetCount`: how many people the user wants added from this search. **Always confirm before searching** (see step 2) unless the user already gave a number in the request.
- `criteria`: the confirmed search criteria (sector, kinds of companies, exclusions, seniority, geography, stage). Always confirm these with the user in step 2. Never assume them silently.
- `sheet`: the Google Sheet to write into. Default is the user's existing sheet **"Vertical AI Agent Founders"**: `https://docs.google.com/spreadsheets/d/1K-T3XaVf3XiMwrjHdgOJB2dTn0H-tMywLwn1smaxPcE/edit`. **Always write into this same sheet. Never create a new one** unless the user explicitly gives a different sheet.

## Sheet columns (written by name, never by position)

Columns the skill fills: `Company Name | Title | Full Name | Sector | What they build | LinkedIn URL | Importance | Reason | Reference Company`

**There is no Rank or Status column.** Never create, write, read or expect one. Prioritisation is the **Importance** column only. Do not write any status label (`Verified fit`, `Close call`, `Not a fit`, numbers, `1-Great Fit`, etc.); if a judgement needs explaining (e.g. "judged from headline only"), put it in Reason.

**The user edits and re-sorts this sheet by hand.** So on every run:
- Read the header row (row 1) fresh and build a map of column name → column letter. Write each value under its column by name. The column order, and extra columns the user added, can change at any time.
- If one of the skill's columns is missing from the header, append that header name in the first empty column of row 1 (never insert or move columns). Leave any columns the user added blank in new rows.
- Match people by normalised LinkedIn URL only, never by row number.
- New people are **appended at the bottom**. Never insert rows, never re-sort, never clear the tab, never rewrite or move existing rows.
- Never edit an existing person's row unless the user explicitly asks; if they do, re-read the sheet right before writing, find the row by LinkedIn URL, and update only the named cells.

- **Sector**: short label such as `AI insurance`, `AI legal`, `AI finance / accounting`, `AI healthcare RCM`, `AI ecommerce ops`, `AI PR`, `AI IT ops`, `AI logistics`.
- **What they build**: one plain sentence on what the agent does and for whom.
- **Importance**: `High`, `Medium` or `Low`.
  - **High:** a close match to the confirmed fit profile, the agent clearly acts inside websites or apps it doesn't own, and the person is a founder, CEO or CTO. Archetype matches (vertical agent for prosumers or small businesses, no in-house computer use, especially with signs they already use or struggle with a third-party provider) go to the top of High.
  - **Medium:** a close match where how the agent works is unclear (a close call), or a close match with a VP or Head-level person, or a looser match with a founder whose agent clearly acts inside other software.
  - **Low:** a looser match to the fit profile, an agent that mostly talks or analyses, or an early lead rather than a decision-maker.
- **Reference Company**: the company the user selected for this search (the input `target`'s company, e.g. `Echelon AI`). If the input was a person, use their company, optionally with the person's name in brackets: `Echelon AI (Eddie Guo)`. Fill it on every row this run adds, so the user can filter the sheet by search.
- **Reason**: one or two sentences covering why they are relevant (or not) and why they got that importance. Example: "Co-founder & CEO of a YC S23 healthcare billing agent; payer-portal work implies browser automation. High: top decision-maker at a strong-fit company."

**Header names to recognise** (the user may rename): treat `Name` as Full Name, `Company` as Company Name, `Why included / left out` as Reason. If the header has a `Rank` or `Status` column, ignore it: never write to it, never remove it yourself.

## Procedure

1. **Understand the input company first.** Spend a couple of minutes on this. It is reading, not searching for people yet.
   - LinkedIn profile: read it for the person's current company and role.
   - Company URL: open the site (homepage plus product or about page).
   - Company name: run a quick Google search, then open the site, plus its YC or Crunchbase page if one exists.
   - Write down its **characteristics**:
     - what the company does, in one or two plain sentences
     - who it sells to
     - its sector or category (e.g. AI insurance ops)
     - the workflow the agent automates
     - where the agent acts: which websites, portals or apps it probably has to operate, and why
     - business model and product shape
     - stage, size, funding and location if visible
   - Check whether the company matches the **ideal customer archetype** (above), and note the evidence.
   - Turn these into a **fit profile**: the three to six traits a similar company should share, marked must-have or nice-to-have. If the company matches the archetype, include it as a must-have. Add the fixed rules: no computer-use sellers, a strong preference for agents acting inside other software, and size similar to the selected company.
   - Boil the company down to **3–5 short search phrases**, each a few words (about 2–6) that work as a LinkedIn keyword search on their own, covering *different ways people describe the same space* (category name, the platform or workflow, industry jargon or acronym, "agentic …" phrasing, a broader adjacent framing). No product details, no customers, no "that do X inside Y for Z" clauses. Too specific: "AI agents that do the hands-on work inside enterprise software (like ServiceNow and SAP) for companies". For Echelon AI: `AI agents for IT operations`, `AI ServiceNow agent`, `AI IT service management`, `agentic ITSM`, `AI enterprise workflow agent`.
   - Keep the detailed characteristics and fit profile for your own judging only; they are never shown in the confirmation card and never used as search keywords.

2. **Confirm with the user before any search. Do not search until they confirm.** The card shows only the **list of search phrases** and the **target count** (plus optional extra criteria). Nothing else: no fit profile, customer names or funding. The user can keep, remove, edit or add phrases. Use a multi-select so they can untick phrases, and the free-text box for edits and additions:

   ```javascript
   var [kept, extra, count] = await askChoice({ questions: [
     { message: 'Search phrases for ' + companyName + ' (each used for one Google search and one LinkedIn people search). Untick any to drop. To edit or add, type the full list you want, one phrase per line or comma-separated.',
       options: phrases, multiple: true },
     { message: 'Any other criteria? (Pick any, or type your own.)',
       options: ['US only', 'Seed / Series A only', 'YC-backed only', 'Founders and CEOs only', 'Include adjacent verticals', 'No extra criteria'], multiple: true },
     { message: 'How many people do you want on the list from this search?', options: ['10', '20', '30', '50'] },
   ] })
   var targetCount = parseInt(String(count || '').match(/\d+/)?.[0] || '20', 10)
   ```

   - **Resolving the confirmed list:** ticked options are kept as-is. If they typed text, treat it as phrases (split on new lines or commas). If the typed text is clearly a full list, it replaces the list; if it reads as additions or edits ("add X", "change Y to Z"), apply them to the ticked set. Use every phrase exactly as written: don't rephrase, extend or "improve" it. If their reply is an instruction rather than phrases (e.g. "broader"), generate a new list and confirm again before searching. If the result is ambiguous, show the resolved list once more with `askUser` before running.
   - **For every confirmed phrase, run BOTH a Google search and a LinkedIn people search, verbatim** (no added words like "founder"; seniority is handled in triage). Never skip either source, even if one source alone could reach the target. Pool the candidates from both sources and all phrases, remove duplicates by normalised LinkedIn URL, then pick up to the target count from the combined pool. Don't invent new phrases without asking; if the combined pool has fewer fits than the target, report the shortfall (or ask to add phrases).
   - Fold extra criteria (e.g. US only) into LinkedIn filters (location filter, not extra words in the keyword), into the triage and judging prompt, and into the Reason text.
   - Skip the count question only when the request already gave a number. The description must always be confirmed. If the card is dismissed, ask once more with `askUser`; if there is still no answer, do not search. Use `pauseForUser` with the proposed description and count.
   - `targetCount` is the most people this run appends, picked from the combined Google + LinkedIn pool. Not-a-fit candidates aren't written and don't count.
3. **Load the sheet and its header.**
   - `google.sheets.getSpreadsheet` gives you the first tab title.
   - `getValues` on `'<tab>'!A1:ZZ5000` gives you the header row and existing rows.
   - Build the column map from row 1 (`colOf(name)`, see helper). Add any missing skill column header in the first empty header cell only.
   - Build a dedupe set of normalised LinkedIn URLs (lower-case, strip query string and trailing slash) from the `LinkedIn URL` column found by name, plus a `full name|company` key as a fallback.
3b. **Google search (always, for every phrase).** Google and LinkedIn are equal sources: both always run for every confirmed phrase, and neither is a top-up for the other.
   - **One Google search per confirmed phrase, and nothing else.** The query is the confirmed phrase exactly as confirmed: plain text, **no quotation marks**, and **never the selected company's name** (no `<Company> competitors`, `<Company> alternatives`, `companies like <Company>`, and no company name attached to any phrase). Example for Echelon AI: `AI agents for IT operations`, `AI ServiceNow agent`, `AI IT service management`, `agentic ITSM`, `AI enterprise workflow agent`.
   - Run every confirmed phrase. Don't stop early, even if Google alone has found enough candidates.
   - plus the YC directory for each confirmed phrase: `ycombinator.com/companies?query=<phrase>`
   - The confirmation card (step 2) already shows the phrases; tell the user each phrase is used for one Google search and one LinkedIn people search.
   - From the results (top ~10 per query, plus comparison/listicle pages such as G2, Crunchbase, "top X" articles), collect candidate **companies**. Drop the selected company itself, computer-use sellers, and companies clearly unlike the fit profile.
   - For each candidate company, get the founder/CEO/CTO and their LinkedIn URL from the company's own site, its YC page, or Crunchbase. If no link is listed there, one LinkedIn people search for `<Company name> founder` is allowed; open the profile only if the headline doesn't settle it (read-only).
   - Add each person to the **candidate pool** (not straight to the sheet) with source `Google` and the query that found them. Dedupe the pool by normalised LinkedIn URL against the sheet and within the pool; save the pool to `tmp/`.
   - Always continue to LinkedIn (step 4), whatever the pool size.

4. **LinkedIn people search (always, for every phrase): choose the page depth from `targetCount`.**
   - URL: `https://www.linkedin.com/search/results/people/?keywords=<urlencoded>&page=<N>`.
   - `<urlencoded>` is a confirmed phrase exactly as confirmed. One search per phrase; page through its results.
   - **How many pages:** a results page has about 10 people, and usually only 1–3 of them fit. Start with pages per phrase ≈ `ceil(targetCount / (number of phrases × 2))`, at least 1 and at most 10. Rotate across phrases (page 1 of each, then page 2 of each, …) so the pool draws from all of them. Go deeper on phrases still producing fits; stop paging a phrase once a page yields nothing new or relevant.
   - **Pool and dedupe:** add each person to the same candidate pool with source `LinkedIn`. If they are already in the pool from Google (same normalised LinkedIn URL), mark their source `Both` instead of adding a second entry. Skip anyone already in the sheet.
   - **Run at least page 1 of every confirmed phrase**, whatever the pool size. Stop paging once the combined pool holds clearly more fits than the target (about 1.5×), or a phrase runs dry. If the pool is still short after all phrases, report the shortfall honestly.
   - Wait about 5 seconds after each navigation, snapshot, and parse the result rows (helper below).
   - **Triage on the headline. Don't open every profile.**
     - Clearly irrelevant (not a founder or lead, clearly unlike the confirmed fit profile, or selling computer use): skip. Don't write them to the sheet.
     - Clearly relevant (e.g. "Co-founder & CEO @ X (YC S24) | AI agents for insurance ops"): add with an Importance (note "from headline" in Reason), or open the profile when the High/Medium call depends on it.
     - Promising but ambiguous: open the profile, judge it against the company preference (use `callLLM` on the profile text and ignore the "More profiles" sidebar), and either add it with an Importance or drop it. Borderline cases get Medium or Low with the doubt explained in Reason.
   - Skip anyone already in the dedupe set **before** opening their profile.
5. **Pick from the combined pool and write.** After both sources have run for every phrase, take the fits in the pool (dropping not-a-fits), rank by Importance (High, then Medium, then Low; within a level prefer source `Both`, then stronger evidence and seniority), and pick up to `targetCount`. Start each Reason with its source: `Source: Google (<query>).`, `Source: LinkedIn (<phrase>).` or `Source: Google + LinkedIn (<query/phrase>).` Re-read the header row, build each row by column name (`buildRow`, see helper), re-check the dedupe set against the sheet, and `appendValues` at the bottom. Save the pool and progress to `tmp/` throughout, since the REPL can reset mid-run, and nothing should be lost or written twice.
6. **Both sources always run.** Never skip Google or LinkedIn for any confirmed phrase, even if one source alone could reach the target.
7. **Report (no re-ranking, no sorting).** Every row you appended must have an Importance and a Reason. Do not reorder, re-rank or rewrite the sheet. Close with a short receipt:
   - the confirmed company read and criteria, in one line
   - the target versus how many people were added
   - the count by Importance
   - how many people came from Google, LinkedIn, or both
   - the confirmed phrases and how many pages each was searched
   - the top High-importance names
   - the sheet link

## Rules

- **LinkedIn is read-only:** no connect, follow, message or react. Opening a profile notifies the person if the user isn't in private mode, which is one more reason to open only the profiles that need it.
- **Keep it moving.** The user wants speed. Work straight from the results lists, don't re-search people you already saw, and don't re-check rows already in the sheet.
- **Never write a duplicate.** Check the dedupe set right before every append.
- **Never create a second sheet.** If the default sheet can't be opened, ask the user (askUser) rather than making a new one.

## Helpers

```javascript
// Parse one LinkedIn people-search results page (React SDUI). Returns [{name, headline, url, snippet}]
function parseResults(snap) {
  var o = snap.snapshot.outline()
  var main = o.slice(Math.max(0, o.indexOf('## region: Primary content')))
  var out = []
  for (var c of main.split('[item: listitem]').slice(1)) {
    var m = c.match(/\[link: (.+?) • (?:1st|2nd|3rd\+) (.+?)\]\(ref=e\d+ → (https:\/\/www\.linkedin\.com\/in\/[^\/)?]+)/)
    if (!m) continue
    var ai = (c.match(/### img: AI generated\n([^\[]+)/) || [])[1] || ''
    out.push({ name: m[1].replace(/ (Premium|Verified)$/, ''), headline: m[2], url: m[3], snippet: ai.trim().slice(0, 200) })
  }
  return out
}
var norm = u => String(u || '').toLowerCase().split('?')[0].replace(/\/+$/, '')

// Judge an opened profile against the company preference
async function judgeProfile(page, person) {
  await page.goto({ url: person.url + '/', referer: 'https://www.linkedin.com/search/results/people/' })
  await wait({ waitTime: 5 })
  var o = (await page.snapshot()).snapshot.outline().replace(/\(ref=e\d+[^)]*\)/g, '')
  var i = Math.max(0, o.indexOf(person.name.split(' ')[0]) - 200)
  var r = await callLLM({ prompt: 'LinkedIn profile of ' + person.name + '. Ignore sidebars and other people\'s posts. Using this confirmed fit profile and these rules: <paste the confirmed fit profile, the hard rule, the act-inside-software preference, the size rule and the person preference>. Return ONLY JSON {"company","title","sector","what","fit":true|false,"importance":"High|Medium|Low","reason"}. (fit=false → don't write the person; fit=true → append with this Importance. Add Reference Company yourself from the run's target.)\n\n' + o.slice(i, i + 18000) })
  return JSON.parse(r.replace(/```json|```/g, '').trim())
}

// Header-driven writing: always re-read row 1, never assume positions
var ALIASES = { 'Full Name': ['Full Name', 'Name'], 'Company Name': ['Company Name', 'Company'], 'Reason': ['Reason', 'Why included / left out'] }
async function readHeader(SID, TAB) {
  var h = (await google.sheets.getValues({ spreadsheetId: SID, range: "'" + TAB + "'!1:1" }))[0] || []
  return h.map(x => String(x || '').trim())
}
function colOf(header, name) {
  var names = ALIASES[name] || [name]
  return header.findIndex(h => names.some(n => n.toLowerCase() === h.toLowerCase()))  // -1 if missing
}
// person: { 'Company Name', 'Title', 'Full Name', 'Sector', 'What they build', 'LinkedIn URL', 'Importance', 'Reason', 'Reference Company' }
function buildRow(header, person) {
  var row = new Array(header.length).fill('')
  for (var k in person) { var c = colOf(header, k); if (c >= 0) row[c] = person[k] }
  return row  // append with google.sheets.appendValues at the bottom; never updateValues over existing rows
}
```

If the parser returns nothing, LinkedIn's markup probably changed. Read `snap.snapshot.outline()` for one page and adjust the regex. The LinkedIn skill (`c0df2d40-d202-4be0-b3c3-c9624c79d65d`) covers LinkedIn page structure if you need more.
