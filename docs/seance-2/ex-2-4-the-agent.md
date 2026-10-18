# Ex 2.4 — The AI Agent 🤖

**Goal**: get **the same result as in 2.2**, but with an Agent. So that you know from
experience when an agent is worth it, and when it costs you.

**What you learn**: the difference between a node that *executes* and a node that *decides*.

**You duplicate your 2.2 workflow.** Do not replace it. Keep the original to compare.

!!! info "This exercise is the centre of the module"
    Your Séance 3 project **must** contain at least one real AI Agent node. This is where
    you learn what that actually means.

## The idea, in one picture

A **chain** (your Basic LLM Chain from 2.2) follows the pipe you drew: data → prompt →
answer. Always the same order, always the same number of calls.

An **Agent** receives a **mission** and a **toolbox**. It **decides by itself** what to
call, in what order, and how many times. More powerful. Less predictable. Those two things
always come together.

## CP1 — The agent answers

1. Duplicate your 2.2 workflow (right-click → Duplicate). Work on the copy.
2. Replace the **Basic LLM Chain** node with an **AI Agent** node (search "Agent"). Rewire
   the same model node (**OpenRouter Chat Model**, credential `Workshop LLM`).
3. Rewrite your prompt as a **mission**, not a rigid instruction:
   ```
   You are a market analyst for FoodFleet, a B2B lunch-delivery startup.
   Your mission: [summarise / classify / draft / score] the data you are given,
   following these rules: [your rules].
   ```
4. Execute with a test input.

✅ **Done when**: the agent answers, in the same spirit as your 2.2 chain. → CP1.

??? tip "Want a reference to compare against?"
    [`s9-assistant-agent.json`](../skeletons/s9-assistant-agent.json) is a complete working
    agent workflow with a tool already wired. Import it in a separate workflow and read it.
    Do not copy it into your own: build yours, then compare.

## CP2 — Give it a tool

Wire **one** tool, as readable as possible: a **Google Sheets Tool** node set to **read**
your own sheet ("check whether this lead already exists").

Then open the execution and go to the **Logs** tab (or the Agent node detail view). This is
where the real exercise happens: **watch the agent decide**. You see the order in which it
called the model and the tool, and why.

✅ **Done when**: in the logs, you can point at the exact moment the agent called your tool,
and say why it called it there. → CP2.

??? tip "Hint 1"
    The agent never calls the tool? The tool's **name and description** are what the agent
    reads to decide whether it needs it. Not the technical config. Write an explicit
    description: "Use this tool to check whether this lead already exists in our CRM before
    answering."

??? tip "Hint 2"
    `iterations limit` error? That is intentional and healthy. A boxed-in agent keeps
    looking for a solution it was never given. Reduce the request or add the missing tool.
    Do not raise the limit as your first move.

## CP3 — See the cost of the freedom

Run the **same input 3 times**. Write down what you observe:

1. **The cost varies** — the number of model calls is not the same from run to run.
2. **The output varies** — the stable format you achieved in 2.2 is harder to hold.
3. **The failures are a different kind** — not "misspelled field", but "it did not call the
   right tool". Much harder to debug than an empty field.

✅ **Done when**: you have three observations written down, with numbers where you have
them. → CP3.

## CP4 — Write your decision rule

One sentence: *"For this use case, chain / agent, because ____."*

That sentence is the real deliverable of this exercise. Not the workflow.

✅ **Done when**: your rule is written. → CP4. 🎉

---

!!! warning "The trap of the demo that impresses"
    An agent impresses in a demo and disappoints in production: more latency, more cost,
    more ways to fail silently. In Séance 4, "it really runs" counts more than "it is
    sophisticated".

    Your project needs one agent node — but it needs that agent to be **justified**. "I used
    an agent because the task needs a decision I cannot draw as a pipe" is a good answer.
    "I used an agent because it was in the brief" is not.

!!! note "Budget"
    Same `Workshop LLM` credential, same $1 cap. An agent makes **several** calls per run.
    Do not wire it to a fast Schedule Trigger while you experiment. After the module you can
    use your own keys.
