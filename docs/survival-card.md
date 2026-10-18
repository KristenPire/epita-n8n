# n8n survival card

> Keep this tab open next to n8n. All the vocabulary of the module is here.

## Words

| Word | What it means |
|---|---|
| **Node** | One box on the canvas = one step ("fetch this", "send that") |
| **Workflow** | The whole chain of boxes, left to right |
| **Trigger** | The node that *starts* the workflow (a clock, a form, an event) |
| **Webhook** | A URL. When something outside calls it, your workflow starts |
| **API** | A door a service opens, so your workflow can ask it for data |
| **JSON** | The data format: objects inside objects, each with a key |
| **Payload** | The data that just arrived |
| **Field** | A key and its value in the JSON (`name: "Camille"`) |
| **Item** | One record of data. A node can process 1 item or 200 items in one run |
| **Credential** | A login or key stored in n8n. You *select* it from a list. You never retype it |
| **Expression** | A formula field. Anything inside `{{ }}` is replaced by real data |
| **Execution** | ONE run of your workflow. Click it to see what each step did |
| **Filter / IF** | A node that lets some items pass and blocks the others |
| **Merge** | A node that joins two streams of data into one |
| **Rate limit** | The API says "too many calls, slow down". Wait, or space out the calls |
| **LLM Chain** | An AI node that always does the same thing: prompt in, text out |
| **Agent** | An AI node with a mission and tools. It **decides by itself** what to call, and in what order |
| **Tool** | A capability you plug into an Agent — read a sheet, call an API. The agent chooses to use it or not |

## The 5 useful formulas

```
{{ $json.name }}
```
→ the `name` field from the previous node

```
{{ $json.company.city }}
```
→ a field inside a field

```
{{ $json.hits[0].title }}
```
→ the FIRST element of a list — **lists start at 0**

```
{{ $now.format('dd/MM') }}
```
→ today's date

```
{{ $json.email || "no email" }}
```
→ a fallback value when the field is empty

---

## The 2 reflexes

1. 🔴 **Red node?** Open it. Read the **first line** of the error. Only the first line.
2. 🤔 **Not sure of a field name?** Open the **previous** node. Look at its **OUTPUT**
   panel. The answer is always there.

## One more thing about `undefined`

A field name that does not exist does **not** give a red error. It gives an **empty**
string. The node stays green. This is the most common bug in this module.
