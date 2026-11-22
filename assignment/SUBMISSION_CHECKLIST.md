# Submission checklist

Tick every line before you submit. Your trainer will not accept an incomplete repository.

## Repository

- [ ] Repository is named `kaveri-<team-name>` and the trainer has access
- [ ] Folder structure matches `starter_repo/` (sql, data_model, agents, tests, docs)
- [ ] `README.md` lets someone else run your work from scratch, step by step
- [ ] No passwords, keys or `.env` files in the repository
- [ ] No real personal data. Customer emails are masked anywhere they appear
- [ ] `.gitignore` is present and excludes `.env`

## SQL (`sql/`)

- [ ] `01_load_data.sql` loads all four team folders
- [ ] `02_profile.sql` shows the counts and issues you found
- [ ] `03_linking_rules.sql` documents each mapping rule as a query
- [ ] `04_order_delivery_invoice.sql` runs without errors on a fresh load
- [ ] The main query's row count and flag count are written in `README.md`

## Data model (`data_model/`)

- [ ] `normalized.dbml` pastes into dbdiagram.io without errors
- [ ] `star.dbml` pastes into dbdiagram.io without errors
- [ ] Every table has a primary key, and every link is a foreign key
- [ ] `diagrams.png` shows both models

## AI helpers (`agents/`)

- [ ] At least two helpers, with a clear job for each (`agents/README.md`)
- [ ] The match or hold rule is code, not a prompt
- [ ] No helper approves, pays, changes an invoice or messages a customer by itself
- [ ] Customer emails are masked before any AI model sees them
- [ ] Every decision is written to a log, with evidence and a timestamp
- [ ] The helpers run on the real dummy data, and the output is shown in `README.md`

## Tests (`tests/`)

- [ ] At least five tests for your rules
- [ ] Tests include at least one edge case (a value exactly on the limit)
- [ ] All tests pass when you run them, and the command is in `README.md`

## Documents (`docs/`)

- [ ] `problem_statement.md` is written
- [ ] `architecture.md` has a diagram and a written description
- [ ] `issues_log.md` lists at least five real data problems, and how you handled each

## AI use and reflection

- [ ] `PROMPT_LOG.md` has an entry for each AI prompt you used for building
- [ ] Each log entry says what you kept, what you changed, and whether it worked
- [ ] `REFLECTION.md` starts with the declaration and your name
- [ ] `REFLECTION.md` was written by hand, with no AI tools

## Demo

- [ ] Demo video or live slot is booked, and it lasts no more than 10 minutes
- [ ] The demo shows the model, one query, one helper run with its log, and the human step
- [ ] You can answer questions about each part without looking at AI output

## Last step

- [ ] You have tested the README steps on a clean copy of the repository
- [ ] You have deleted the Azure resource group if you created one (Setup 02, Step 6)
