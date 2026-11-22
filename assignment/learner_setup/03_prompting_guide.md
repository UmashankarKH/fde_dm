# Setup 03: How to prompt an AI assistant for this project

**Goal:** get useful code and explanations from an AI tool, check them, and keep a record of what you asked.

**Tools you may use:** Claude, ChatGPT, GitHub Copilot, Gemini, or any other AI assistant. Open-source local models are also fine. The tool name doesn't matter as much as how you use it.

---

## The three rules

1. **Never paste secrets or real personal data.** No passwords, keys, real customer emails or real client records. Mask emails first, for example `s***@example.com`.
2. **Check every answer.** Run the code. Read the SQL before you trust its output. If a number looks wrong, it probably is.
3. **Log your prompts.** Add every prompt you use for building to `PROMPT_LOG.md` in your repository (format below).

**Important:** AI helps you build. It must **not** write your reflection. See `REFLECTION_QUESTIONS.md`.

---

## What a good prompt contains

Think of a prompt as a brief to a new team member. Give them:

| Part | What it means | Example |
|---|---|---|
| **Role** | Who the AI should act as | "You are a data engineer reviewing SQL." |
| **Context** | What the project is | "We have four MySQL tables from a distributor. There is no shared key." |
| **Data** | The real structure, with fake sample rows | Paste the column names and three sample rows (masked) |
| **Task** | One clear thing to do | "Write a query that links orders to deliveries." |
| **Constraints** | What must be true | "Do not change the raw tables. Use MySQL 8 syntax." |
| **Output** | What the answer should look like | "Return the SQL, then a two-line explanation of each join." |

### Template

```
Role: You are a [data engineer / Python developer / SQL reviewer].
Context: [one or two sentences about the project].
Data: [column names, types, and 3 masked sample rows].
Task: [one specific thing].
Constraints: [what must not happen, what version to use].
Output: [code only / code and explanation / a table].
```

---

## Example: a good prompt

```
Role: You are a data engineer who writes clear MySQL 8 queries.
Context: Kaveri Kitchen has order numbers like SO-1001 in the sales table
and SO1001 (no dash) in the warehouse deliveries table. There is no shared key.
Data:
  raw_sales.orders: order_id (e.g. 'SO-1001'), customer_email (masked), qty
  raw_warehouse.deliveries: order_ref (e.g. 'SO1001'), sku, delivered_qty
Task: Write a query that links each sales order to its deliveries, using a
normalised order number. Show orders with no delivery.
Constraints: Do not change the raw tables. Use a CTE for the normalised key.
Output: The SQL, then one sentence on what the normalisation rule is.
```

## Example: a weak prompt (and why)

> "Make me a model for my data and fix everything."

It has no context, no data, no task and no output format. The answer will be generic and may be wrong for your data. Ask for one thing at a time.

---

## Follow-up prompts that work well

- "Show me the SQL you would run to check this result, and the number you expect."
- "What assumptions did you make? List them."
- "Write three tests that would catch a wrong answer here."
- "Explain this code line by line, as if to a new team member."
- "This output is wrong. Here is the output and the expected result. Find the cause."

---

## Prompting for the AI helpers

Build the rules as code first, then ask the AI to help with the wrapper.

Good: "Write a Python function `reconcile(billed_qty, delivered_qty, tolerance)` that returns MATCH or REVIEW. Add 5 unit tests, including the edge case where the difference equals the tolerance."

Weak: "Make an agent that checks invoices and decides if they are correct."

The second version lets the AI decide the arithmetic. Your rules must be testable code.

---

## Keep a prompt log

Create `PROMPT_LOG.md` in your repository, and add an entry for each prompt you use:

```markdown
## 2026-11-24 · SQL linking rule
- **Tool:** Claude (or whichever you used)
- **Prompt (masked):** [paste the prompt, with any personal data masked]
- **What I used:** [the code I kept, and where it lives]
- **What I changed and why:** [e.g. "changed the join to LEFT JOIN, because 4 orders have no delivery"]
- **Did it work?** [yes / partly / no, and the evidence]
```

A clear log shows your thinking. It is also how your trainer sees which tool helped and where it failed.

---

## When the AI is wrong

It will sometimes be wrong, and confidently so. Check it by:
1. Running the query and comparing with a count you can do by hand.
2. Checking a single example row, end to end.
3. Asking it to show the evidence, then checking the evidence yourself.

Write down the mistake in your `issues_log.md`. Mistakes are part of what gets marked.
