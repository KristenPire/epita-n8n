# Ex 2.2 — The Analyst 🧠

**Goal**: your data stream goes through an AI that analyses it, and the result lands
somewhere useful.

**What you learn**: AI as an ordinary transformation node, writing a prompt that returns a
**stable format**, landing in a structured destination.

**You extend YOUR 2.1 workflow.** Do not start a new one.

!!! info "This is the first half of what an agent is"
    An LLM step like this one always does the same thing, in the same order. It is a
    function. In 2.4 you replace it with something that **decides**. Build this one well
    first: it is the baseline you compare against.

## Pick YOUR analyst mission (only one)

| Mission | What the AI does | Pick it if… |
|---|---|---|
| **Summarise** | 10 articles → 1 digest, 5 lines, readable in 30 seconds | the value is in reading less |
| **Classify** | each item → a label (`hot/warm/cold`, `relevant/noise`) | the value is in sorting |
| **Draft** | one data item → text ready to send (email, post) | the value is in writing less |
| **Score** | each item → a score 1–10 + a one-sentence reason | the value is in prioritising a stream that is too big |

## CP1 — The AI answers you (dry run)

1. At the end of your 2.1 workflow, add a **Basic LLM Chain** node (search "LLM"). Model:
   select the **`Workshop LLM`** credential.
2. Hardcoded test prompt: `Reply only: OK`. Execute.

✅ **Done when**: the AI answers. That was your first LLM call from a workflow. → CP1.

!!! warning "💸 Budget"
    Each call costs a fraction of a cent. Your budget for the module is $1. You cannot
    break anything — unless you set a trigger every 10 seconds. Do not set a trigger every
    10 seconds.

## CP2 — Your real data enters the prompt

Replace the test prompt with a real prompt, **with your data injected by expression**. This
structure works. Adapt it to your mission:

```
You are a market analyst for FoodFleet, a B2B lunch-delivery startup.

Here is raw data:
Title: {{ $json.title }}
Source: {{ $json.source }}
Date: {{ $json.date }}

Your task: [summarise / classify / draft / score] using these rules:
- [rule 1 — be precise]
- [rule 2]

REQUIRED output format:
[describe the exact shape: "3 lines maximum", "only one of these words:
HOT, WARM, COLD", "JSON: {"score": X, "reason": "..."}"]

If the data is empty or makes no sense, reply exactly: INVALID_DATA
```

✅ **Done when**: the answer talks about your real data AND respects your format, 3 runs in
a row. → CP2.

??? tip "Hint 1"
    Answer ignoring your format? Make the format section blunter. Give a literal example of
    the expected output. LLMs imitate better than they obey.

??? tip "Hint 2"
    Your node receives 15 items → 15 AI calls, one per item. That is correct for
    classify/score. For a single DIGEST you must group first: **Aggregate** node before the
    LLM.

??? tip "Hint 3 — for the engineers"
    Want the output parsed, not just text? Wire a **Structured Output Parser** to the chain
    and give it a JSON schema. You get typed fields instead of a string you have to regex.
    This is also the right answer when the next node needs a real number.

## CP3 — The result lands cleanly

Pick ONE destination and wire it after the AI:

- **Slack**: the digest in `#news`, items classified `HOT` in `#leads`
- **Google Sheets**: one row per analysed item (date, title, AI verdict). The start of a
  database

✅ **Done when**: the final result is where you decided, formatted, usable by someone who
has never seen your canvas. → CP3.

## CP4 — Full chain, real conditions

Replace the Manual Trigger with a **Schedule Trigger** (any time you want) and switch to
**Active**.

✅ **Done when**: live data → AI → destination, without you. → CP4. 🎉

---

!!! success "Finished early?"
    - Add a **confidence** field to the AI output, then a Filter: low confidence goes to a
      "needs a human" destination instead of the main one. That is the cheapest form of
      human-in-the-loop, and it earns points in Séance 4.
    - Compare two different prompts on the same 10 items. Which one is more stable?
