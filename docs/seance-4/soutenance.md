# Séance 4 — Soutenance 🎤

**This is the exam.** You present **alone**, your own project. Everyone in the room watches.

**Format**: 8 minutes of presentation + 4 minutes of questions. Hard cutoff at 8:00. A timer
is projected.

The two things graded are the two from the module brief: **you explain how it works**, and
**you justify why it is relevant**.

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

---

## Questions you should expect

Prepare an answer for each of these. They will be asked.

- **"Why an agent and not a simple rule or a fixed LLM chain?"** — the most common question.
  If the honest answer is "a rule would have been enough", say so. Recognising it scores
  better than defending a bad choice.
- **"What happens if this API is down tomorrow?"**
- **"What happens if you run it twice?"**
- **"Where is this field coming from?"** — pointing at a random node on your canvas.
- **"What does it cost per run?"** — a rough number is fine. Know whether it is cents or
  euros.
- **"Would you let it act without you checking?"** — your Ex 2.3 paragraph answers this.
  Reuse it.
- **"What broke the most while you were building it?"** — an honest answer here is worth more
  than a polished one.

---

## If it breaks live

Breathe. Neither option below is a failure.

1. **Debug out loud for 20 seconds.** Say what you are reading, in the error, in the logs.
   This is often the best moment of a soutenance: we see you work.
2. **Play your 60-second screencast** and keep narrating over it.

What loses points is pretending nothing happened, or going silent.

---

## Practical

- Bring your **own laptop**, charged. Test the projector connection before your slot.
- Have the **screencast** on the machine, not in the cloud. Assume the WiFi fails.
- Have the **execution history** open in a tab: a successful past execution is your proof if
  the live run fails.
- **No slides required.** The canvas and the real output are your slides. If you want one
  slide, make it the problem and its number.

!!! success "The point of all this"
    At the end you have one automation that runs on your own accounts, that you understand
    completely, and that will still be running next month. That is worth more than the
    grade.
