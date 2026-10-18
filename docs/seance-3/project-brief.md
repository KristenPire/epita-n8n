# Séance 3 — Project Brief 🚀

**This is the graded project.** You work **alone**. You have 2 hours in class to start, then
**2 weeks** on your own. You present it in [Séance 4](../seance-4/soutenance.md).

FoodFleet is finished. From now on you build **your** project.

---

## How to choose

This is **not** a "invent anything you like" brief. Open invention is where projects go to
die: two weeks is short, and a vague idea eats all of it.

So:

1. Pick **one family** out of the three below.
2. Pick **one idea** from that family's menu — or an idea close to it, that you can describe
   in one sentence using the same shape.
3. Write your one-sentence pitch and show it to the instructor before you leave the room
   today.

!!! warning "The one condition on your choice"
    You must be able to get **real data** for it, today. Not "when my friend sends me the
    export". Real data, today, from an account you control. If you cannot, change the idea —
    not the deadline.

---

## The production-quality bar (all families)

These three are **requirements**, not bonus points. A project missing one of them cannot get
a good grade, however nice the demo is.

!!! danger "1 — At least one real AI Agent node"
    A **Basic LLM Chain** is not enough. You need an **AI Agent** node with **at least one
    tool** wired to it, and you must be able to show in the execution logs where the agent
    decided to use it. See [Ex 2.4](../seance-2/ex-2-4-the-agent.md).

    And you must be able to justify it. "An agent because the task needs a decision I cannot
    draw as a fixed pipe" is a good justification.

!!! danger "2 — It handles one realistic failure case"
    Pick a failure that can really happen to your workflow and handle it **on purpose**:

    - the API is down or returns a `429` → retry, or a clean error message, not a crash
    - a required field is missing or empty → a fallback, or the item is routed aside
    - the AI answers in the wrong format → a parser plus a "needs a human" branch
    - the workflow runs twice → it must not duplicate anything (Ex 1.4)
    - the workflow has sent nothing for N days → an inverse alert (Ex 1.3)

    In Séance 4 you will be asked to **trigger that failure live**. Choose one you can
    reproduce on demand.

!!! danger "3 — At least one real external service, on your own account"
    Not the `Workshop` credentials. Your own GitHub, your own Gmail, your own Notion, your
    own Google Sheet, your own Telegram bot, a real public API. One is enough.

    A workflow running on the module's shared account is a workflow you cannot keep. One on
    your own accounts still runs next month.

---

## Why every idea below looks too easy

Read any row in the menus: trigger → agent → output, one sentence. That is **on purpose** —
it is the skeleton, not the project. Built exactly as written, most of them are a 2-hour
build, not a 2-week one. That gap is where your actual two weeks go. One worked example,
using Family A's A1:

| | 2-hour version (what the one-liner describes) | 2-week version (what you actually hand in) |
|---|---|---|
| **Trigger** | Manual, you run it when you remember | A real schedule, or a webhook on the form itself |
| **Data** | Read the sheet once, send everything | **Diff against last run** — only enrich and alert on what's new or changed. Dead simple without this; this alone is most of week one |
| **Agent** | One tool: look up the company | **Two or three tools**, and the agent decides which it needs per row — company info, a salary-range lookup, maybe a search for recent news on the company. The decision is the point, not the tools themselves |
| **Failure case** | None — if the sheet has a blank row, it crashes or hallucinates | Handled on purpose: missing field → routed aside, not guessed. API down → retried once, then a clean skip, not a crash |
| **Output** | A flat list in Slack | A digest that **groups and prioritises** — "3 need a follow-up today" before "12 no news yet" |

Same idea. Same family. The difference is entirely in **state across runs**, **more than
one tool for the agent to choose between**, and **a failure case you chose on purpose** —
not a bigger idea. Apply this same stretch to whichever row you pick.

---

## Family A — Your own daily-ops agent 🗂

**Idea**: automate something that is really annoying in your own student life. The test of a
good Family A project is simple: **you will still be using it in March.**

| # | Idea | Shape |
|---|---|---|
| A1 | **Internship / job application tracker** | A form or a sheet collects applications → the agent enriches each one (company, stack, deadline) and sends a weekly digest of what needs a follow-up |
| A2 | **Weekly research digest on one topic** | arXiv + RSS + HN on a topic you care about → the agent filters out the noise, groups by theme, sends 10 lines on Monday morning |
| A3 | **Subscription and spending tracker** | A sheet or email receipts → the agent detects a new charge, an unexpected increase, or a trial about to end, and alerts you |
| A4 | **Inbox or calendar triage agent** | New emails or events → the agent classifies them (act / read later / ignore) and prepares one short daily list |
| A5 | **Study-group coordination bot** | A Telegram or Slack bot: collects availability, decides a slot, posts the recap and the deadlines |
| A6 | **Deadline watcher** | Scrapes or reads the school / scholarship / CFP calendars → the agent alerts you N days before, once, and never twice |

**Where the agent earns its place**: deciding *whether* something needs your attention. A
fixed rule cannot tell "this email needs an answer today" from "this email is a newsletter".

**Where the 2 weeks go**: every row above runs once in 2 hours. The project is making it
track *change over time* (A3's "an unexpected increase" needs last week's number to compare
against — that's state, not a single read) and survive real mess (half your emails won't
fit your categories cleanly on day one).

---

## Family B — Dev and engineering tooling agent 🔧

**Idea**: automate something around software engineering work. The most natural family for
this cohort, and the easiest to demo, because GitHub gives you real events for free.

| # | Idea | Shape |
|---|---|---|
| B1 | **Pull request summariser** | A PR opens (webhook or polling) → the agent reads the diff and posts a plain-language summary plus the risky files, as a comment |
| B2 | **CI failure triage agent** | A build fails → the agent reads the logs, classifies the cause (test / dependency / flaky / infra) and posts a diagnosis with the most likely file |
| B3 | **Changelog / docs agent** | On a tag or on a schedule → the agent reads merged commits and PRs, groups them by type, writes a human changelog and commits it |
| B4 | **Issue triager** | A new issue arrives → the agent labels it, estimates severity, asks for the missing information, routes it to the right person |
| B5 | **Code-review checklist agent** | A PR opens → the agent checks it against *your* team checklist (tests present? migration? secret in the diff?) and reports what is missing |
| B6 | **Dependency / CVE watcher** | On a schedule → read the manifest, check for new versions or advisories, the agent writes what to upgrade first and why |

**Where the agent earns its place**: choosing which tool to call. "Do I need to fetch the
diff, the test logs, or the issue history to answer this?" is exactly an agent decision.

**Technical note**: the GitHub REST API is in the [API Menu](../seance-2/menu-api.md). Get a
personal token: 60 requests per hour without one, 5000 with one.

**Where the 2 weeks go**: a diff is not a PDF — real PRs blow past your prompt's context
window, touch files you shouldn't summarise the same way (a lockfile vs. a logic change),
and arrive with noisy commit history. Handling that, and giving the agent 2-3 tools instead
of 1 (diff + test logs + issue history, not just diff), is the actual project.

---

## Family C — Applied research / data agent 📊

**Idea**: an agent that processes content or data to produce knowledge. The most interesting
family if you are an AI major, and the most demanding one: the quality of the output is the
whole project.

| # | Idea | Shape |
|---|---|---|
| C1 | **Paper summariser + Q&A over a corpus** | A folder or sheet of PDFs → the agent indexes them, and answers questions in Slack with the source document and page |
| C2 | **Dataset quality auditor** | A CSV lands → the agent profiles it, flags missing, malformed and out-of-range rows, writes a short report with the 3 worst problems |
| C3 | **Literature-review assistant** | arXiv query → the agent clusters papers by theme, names each cluster, and tells you which 3 to read first |
| C4 | **Competitive / market-intel analyst** | Two or three public sources on a market → the agent extracts claims, removes duplicates, and writes a weekly brief with the changes since last week |
| C5 | **Meeting notes to action items** | A transcript or a text file → the agent extracts decisions, owners and deadlines, and writes them into a tracker |
| C6 | **Benchmark/leaderboard watcher** | A schedule → read a leaderboard or a results page, the agent explains what changed and whether it matters |

**Where the agent earns its place**: multi-step reasoning with retrieval. The agent decides
how many documents it needs to read before it can answer.

**Technical notes**: n8n has **Default Data Loader**, **Text Splitter**, **Embeddings** and
**Vector Store** nodes. A simple in-memory vector store is enough for C1 and C3 — you do not
need to run a database. And keep the corpus small: 20 papers is a project, 2000 is a
weekend lost to ingestion.

**Where the 2 weeks go**: the first answer your agent gives will be wrong or vague — tuning
retrieval (chunk size, how many chunks to pull, when to say "not enough information" instead
of guessing) is most of the real work, and it is iteration, not a bigger pipeline.

---

## What to do with your 2 hours today

Not "start building". In this order:

| Minutes | What |
|---|---|
| 0–20 | Pick a family and an idea. Write the one-sentence pitch. Show it to the instructor. |
| 20–50 | **Get the data and the access working.** Create the account, get the token, make ONE successful call in an HTTP Request node. Nothing else. |
| 50–80 | Draw the workflow on paper: trigger → steps → agent + its tools → destination. Name the failure case you will handle. |
| 80–110 | Build the **trigger and the first real step** in n8n. One green node with real data beats a beautiful plan. |
| 110–120 | Write down, for yourself: what is the riskiest unknown left? That is what you attack first at home. |

!!! warning "The time trap, budget for it"
    Some OAuth setups (Gmail sending, Meta, HubSpot writing) need the provider to validate
    your app before it leaves test mode. That takes days, not minutes.

    Two ways around it: most providers let the app work in **Test / Development** mode for
    accounts you explicitly add — that is enough for your demo. Or **fall back to a
    stand-in** (a Google Sheet, a Slack message) as the destination, and say so in the
    soutenance: "the Stripe integration needs 3 days of validation, I simulate it with a
    sheet". That is an honest engineering answer, not a failure.

!!! note "Where to find the exact procedure for an API key"
    Not here. Every provider changes its own dance too often. Use the service's **official
    docs** (search "[service] API key"), a **recent video**, or paste your screenshot into an
    AI assistant and let it walk you through the console. Do not stay stuck alone on a cloud
    console screen. That is friction, not the exercise.

## Security, two rules that apply from today

1. Keys and tokens go into a **credential**, never into a node field, never into a Slack
    message, never into a screenshot in your slides.
2. Create the access with **minimum permissions**, on an account you are willing to lose.
    Read-only when read is all you need.

---

## Checklist before Séance 4

- ☐ Switched to **Active**, running on its real trigger — you have watched an execution fire
  by itself
- ☐ Contains an **AI Agent node with at least one tool**, and you can find the decision in
  the logs
- ☐ One **failure case handled on purpose**, and you can trigger it live
- ☐ At least one **external service on your own account**
- ☐ **Re-runnable**: running it twice does not duplicate anything
- ☐ Nodes are **named** — someone else will read your canvas
- ☐ A **60-second screencast** of it working, recorded and saved. The live demo is better,
  but WiFi exists
- ☐ You can say in one sentence **why this use case** and **why an agent**
