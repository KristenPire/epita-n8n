# Defense Day 🎤

**This is the exam.** You present **alone**, your own project. Everyone in the room watches.

**Format**: 8 minutes of presentation + 4 minutes of questions. **Hard cutoff at 8:00** — a
timer is projected, and it applies to everyone, because being kind to the first five
students means the last one presents to an empty room.

The two things graded are the two from the module brief: **you explain how it works**, and
**you justify why it is relevant**.

!!! warning "The one rule to apply before your slot"
    If there is a node in your workflow you cannot explain, **delete it. Before your
    slot.** A simple workflow you fully understand scores higher than a big one you
    cannot explain. Using AI assistants to build was allowed — but if it's on your
    canvas, you own it.

---

## What to come with

Check every box **the evening before**, not in the room.

- ☐ **Your own laptop, charged**, projector tested before your slot.
- ☐ **n8n open, your workflow open**, logged in. Don't spend your 8 minutes finding a
  password.
- ☐ Your **60-second screencast** of a successful run — **on the machine, not in the
  cloud**. Assume the WiFi fails.
- ☐ The **execution history** open in a tab: a successful past execution is your proof
  if the live run fails.
- ☐ A note with your **three main limits**, written down. You will say them yourself.
- ☐ A one-sentence answer to **"would you actually use this next Monday?"** — prepared
  tonight, not improvised.
- ☐ Your rough **monthly cost** number. Know whether it is cents or euros.
- ☐ **No slides required.** The canvas and the real output are your slides. If you want
  one slide, make it the problem and its number.

---

## The 5 beats

| # | Beat | Time | What you say |
|---|---|---|---|
| 1 | **The problem** | 1 min | What was annoying, how often, how long it took. One concrete number. Do not describe the solution yet. |
| 2 | **Live demo** | 2 min | Trigger it in front of us. Real data. We watch the execution and the real output arrive. |
| 3 | **How it works** | 2.5 min | Walk the canvas. One sentence per step. Then stop on the **agent**: its mission, its tools, and show in the logs where it decided to call one. |
| 4 | **Break it on purpose** | 1.5 min | Trigger your failure case live. Show that it does not crash, or that it fails cleanly. This is the beat that separates a demo from a product. |
| 5 | **Limits and next step** | 1 min | What you would not trust it with yet, and the one thing you would build next. |

!!! tip "Rehearse beat 2 and beat 4 with a timer"
    Those are the two that can go wrong on stage. The other three you can talk through from
    memory. Rehearse the fragile 90 seconds, not the whole thing.

**How to narrate the canvas** — one sentence per node, pointing at the screen:

> "The schedule starts it here, every morning at eight." · "This node pulls the new rows." ·
> "The agent gets the goal, and these two tools." · "It chose the second one — you can see
> it in the log, here." · "And the result lands here, in this message."

Two mistakes to avoid: reading every parameter of every node (nobody follows), and *"then
some stuff handles the data"* (that sentence tells us you don't know — expect a question
about exactly that node).

---

## The rubric

| Criterion | Weight | What a good answer looks like |
|---|---|---|
| **It works** | 25% | It runs live, on its real trigger, with real data. A recovered crash is fine. A workflow that only runs in test mode is not. |
| **Functional understanding** | 25% | You explain every node without reading. You can answer "what happens if this node returns nothing?" |
| **The agent is real and justified** | 20% | An AI Agent node with a tool, visible in the logs, and a sentence on why a fixed chain was not enough. |
| **Relevance of the use case** | 15% | A real problem with a real cost. Not a demo looking for a problem. |
| **Robustness** | 10% | The failure case is handled on purpose and shown live. Re-runnable without duplicates. |
| **Clarity** | 5% | 8 minutes respected. Named nodes. The room follows. |

!!! info "What is NOT graded"
    Slide design. Number of nodes. How sophisticated the AI part is. A simple workflow that
    really runs and that you understand completely scores higher than a complicated one you
    cannot explain.

!!! note "The three requirements from Séance 3 are checked"
    A real AI Agent node with a tool · one failure case handled · your own external
    account. If one is missing, **say so yourself at the start**. Do not let it be
    discovered in the questions.

---

## Questions you should expect

Prepare an answer for each of these. They will be asked.

- **"Why an agent and not a simple rule or a fixed LLM chain?"** — the most common question.
  If the honest answer is "a rule would have been enough", say so. Recognising it scores
  better than defending a bad choice. ("Honestly, a chain was enough — the module required
  an agent, so I placed it where it adds the most" is a *good* answer.)
- **"Show me the execution log where the agent made its decision."**
- **"What happens if this API is down tomorrow?"**
- **"What happens if you run it twice?"**
- **"Where is this field coming from?"** — pointing at a random node on your canvas.
- **"What does it cost per run? Per month?"** — a rough number is fine.
- **"Would you let it act without you checking?"** — your Ex 2.3 paragraph answers this.
  Reuse it.
- **"Would you actually use this next Monday?"** — "Yes, because…" is great. "No, honestly,
  because X is missing" is also fine. Hesitating is the only wrong answer.
- **"What broke the most while you were building it?"** — an honest answer here is worth
  more than a polished one.

**On limits, honesty scores:**

| Says nothing | Says engineer |
|---|---|
| "It works" | "It works **for English only**" |
| *(silence about cost)* | "**€4/month** at this rate" |
| "No problems" | "Two runs the same day would duplicate rows — I did not fix that" |

You cannot hide a weakness — it will surface in the questions. But you can show you already
know it. That is the difference between an accident and a decision.

---

## If it breaks live

Breathe. It happens every year. Neither option below is a failure.

1. **Debug out loud for 30 seconds.** Say what you expected, open the output panel, read
   the real data (reflex #1 from Séance 1). This is often the best moment of a defense:
   we see you work.
2. **Play your 60-second screencast** and keep narrating over it. Then move on — do not
   apologise for two minutes.

What loses points is pretending nothing happened, or going silent. You built this. You know
it better than anyone in the room.

---

## When it is not your turn

You are the audience. You will see ~20 different solutions to 20 different problems in one
afternoon — some better than yours. **Take notes.** That is the best part of the day.

---

## After today

1. **Your instance stays yours.** Keep it running if the workflow is useful.
2. **Security hygiene**: delete or rotate the API keys you will not use again. A forgotten
   key in an abandoned project is a real risk.
3. **Keep one workflow alive** — the one you will really use. Automation is only worth
   something when it runs while you are not looking.
4. **This is a real CV project.** Be able to explain it in two minutes, without slides, in
   a job interview.

!!! success "The point of all this"
    At the end you have one automation that runs on your own accounts, that you understand
    completely, and that will still be running next month. That is worth more than the
    grade.
