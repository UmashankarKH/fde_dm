# Assignment: Data Model and AI Helpers for Kaveri Kitchen Supplies

**Duration:** 3 weeks
**Team size:** 2 learners per team (or work alone, same expectations)
**Submit by:** the date your trainer announces
**Read first:** `transcript_kaveri_discovery.md`

---

## 1. The situation

You are the Forward Deployed Engineer (FDE) on the call. The client, Kaveri Kitchen Supplies, has four teams. Each team has its own system and its own data. The teams don't share keys, and they don't have a data model or an ER diagram.

The client has two problems:
- **Overselling:** sales confirms orders for stock that isn't there.
- **Invoice mismatches:** finance bills for more than was delivered.

Your job is to design the data model that links the four teams' data, then build AI helpers that automate **at least one** of these problems.

---

## 2. What you must build

### Part A: Data model (required)

1. **Explore the data.** Load the four team folders into MySQL (see `learner_setup/01_mysql_workbench.md`). Profile every file: row counts, blanks, odd formats.
2. **Write down the problems you find.** At least five. For example: two order number formats, customer identity with no shared key, emails in mixed case.
3. **Design the model.** Draw it on **dbdiagram.io** in DBML. Show:
   - a **normalized** model for the cleaned data (one fact stored once, clear primary and foreign keys)
   - a **star schema** for the question you answer (one fact table, with dimension tables around it)
4. **Write the linking rules.** For example, how a `SO1001` warehouse reference maps to an `SO-1001` sales order. How a customer email maps to a finance customer code. Write each rule as a SQL query or a clear step.
5. **Build the queries.** A SQL script that produces one row per order line, linked to its delivery and its invoice, with a flag where they disagree.

### Part B: AI helpers (required)

Build **at least two helpers** that work together on one problem. Examples:

| Option | Helper 1 | Helper 2 | What a human decides |
|---|---|---|---|
| **Stock check** | Reads live stock and the new order, returns CONFIRM or HOLD with the stock figure used | Writes a short message to Rahul explaining the decision | Rahul approves any HOLD before a customer hears about it |
| **Invoice match** | Compares billed quantity with delivered quantity for each invoice line | Explains each mismatch in plain words and lists the evidence | Pooja approves any change to an invoice |
| **Return finder** | Cleans and standardises the order reference, then finds the order | Suggests the most likely order when the reference is missing | Asha confirms the match before the return is logged |

**Rules for the helpers (these are marked, so read them carefully):**
- The rule that decides a match, a hold or a mismatch must be **code you can test**, not a prompt.
- The AI may explain a result. It must not decide the arithmetic.
- No helper may approve, pay, change an invoice or message a customer on its own.
- Every decision is written to a log, with the evidence and the timestamp.
- Customer emails must be **masked** (for example `s***@example.com`) before any AI model sees them.

### Part C: Working demo (required)

A 10-minute demo, live or recorded, showing:
1. The data model on dbdiagram.io
2. One query run in MySQL Workbench
3. One helper run on a real example from the data, including its log
4. The human decision step

---

## 3. Tools

You may use any **open-source** tool. Examples:

| Job | Suggested tools | Notes |
|---|---|---|
| Database | MySQL Server + MySQL Workbench | Required for the query part (Setup guide 01) |
| Data model | dbdiagram.io | Required for the model drawings |
| Cloud | Azure (free account) | Optional. Setup guide 02 |
| AI helpers | Python with any open-source framework | Your choice. Describe it in the reflection |
| AI assistant for coding | Claude, ChatGPT, GitHub Copilot, or any other | Allowed, but log your prompts (see Setup guide 03) |
| Version control | GitHub | Required |

**Using AI to build is allowed.** Using AI to write the reflection in Section 5 is **not** allowed. See the reflection rules.

---

## 4. Submission: what goes in your GitHub repository

Create a public or invited-access GitHub repository named `kaveri-<your-team-name>`. Use this structure (a starter copy is in `starter_repo/`):

```
kaveri-team-name/
├── README.md                  How to run everything, step by step
├── sql/
│   ├── 01_load_data.sql       How you loaded the four folders
│   ├── 02_profile.sql         Your data profiling queries
│   ├── 03_linking_rules.sql   Your mapping rules (SO-1001 vs SO1001, emails, customer codes)
│   └── 04_order_delivery_invoice.sql   The main linked query
├── data_model/
│   ├── normalized.dbml        Silver model, from dbdiagram.io
│   ├── star.dbml              Gold star schema, from dbdiagram.io
│   └── diagrams.png           Screenshots of both diagrams
├── agents/
│   ├── README.md              What each helper does and its rules
│   ├── helper_1/              Code for helper 1
│   └── helper_2/              Code for helper 2
├── tests/                     Tests for the rules (at least 5)
├── docs/
│   ├── problem_statement.md   Your summary of the client problem
│   ├── architecture.md        Diagram and description of the architecture
│   └── issues_log.md          Problems in the data, and how you handled each one
├── PROMPT_LOG.md              Every AI prompt you used for building, with the date
└── REFLECTION.md              Typed by hand, no AI (see Section 5)
```

**Do not commit:**
- `.env` files or any passwords
- Real personal data (the dummy data is fine)
- Large generated files

---

## 5. The reflection (compulsory, typed by hand, no AI)

The reflection is in `REFLECTION_QUESTIONS.md`. You must answer it **without any AI tool**. That means:
- Don't ask an AI to write, rewrite, correct, translate or summarise any part of it.
- Don't copy from an AI chat, a website or another person's answer.
- Type it yourself, in your own words, from your own understanding.

Your trainer may ask you to explain any answer live. If you can't, the answer will be marked down.

---

## 6. How it is marked

| Area | Points | What we look for |
|---|---|---|
| Data profiling and issues log | 10 | Real problems found, clearly written |
| Data model (normalized and star) | 20 | Correct keys, sensible links, clear diagram |
| Linking rules and SQL | 20 | Queries run, results correct, rules written down |
| AI helpers | 25 | Works on real data, rules tested in code, log written |
| Human decision step and safety | 10 | Masking, no unapproved actions, clear approval |
| Demo | 5 | Clear, honest, shows the real output |
| Reflection (typed by hand) | 10 | Thoughtful, specific, consistent with your work |

**Automatic deductions:**
- Helper approves, pays or changes anything on its own: **-15**
- Customer email shown unmasked to an AI tool: **-10**
- Unexplained AI-written reflection: **the reflection scores 0**
- Results that don't match the data (for example, you claim 11 oversold orders and can't show them): **-5**

---

## 7. Honesty rules

- Say what you did not finish. A clear "not done" is better than a made-up "done".
- Say which AI tools you used and for what. This is not a penalty. Hiding it is.
- Do not try to get the answer key from the instructor folder. It is not in your repository.

---

## 8. Timeline suggestion

| Week | Focus |
|---|---|
| 1 | Load the data, profile it, list the issues, draft the model |
| 2 | Finish the model, linking rules and the main query. Start the helpers |
| 3 | Finish the helpers, tests, documents, demo, reflection |
