# Learner assignment kit: Kaveri Kitchen Supplies

Start here. Read the files in this order.

| Step | File | What it is |
|---|---|---|
| 1 | `transcript_kaveri_discovery.md` | The client call. Read it fully before you do anything. |
| 2 | `ASSIGNMENT_BRIEF.md` | What you must build, the rules, and how it is marked |
| 3 | `learner_setup/01_mysql_workbench.md` | Install MySQL and load the four data folders |
| 4 | `learner_setup/02_azure_setup.md` | Optional cloud setup, with cost guardrails |
| 5 | `learner_setup/03_prompting_guide.md` | How to prompt an AI assistant, and how to log it |
| 6 | `data_learners/README.md` | What every column means, for all four teams |
| 7 | `starter_repo/` | Copy this folder to start your GitHub repository |
| 8 | `SUBMISSION_CHECKLIST.md` | Tick every line before you submit |
| 9 | `REFLECTION_QUESTIONS.md` | Compulsory. Typed by hand, with no AI |

## Folder map

```
assignment/
├── transcript_kaveri_discovery.md   the client call (learners)
├── ASSIGNMENT_BRIEF.md              the task and marking (learners)
├── README.md                        this index
├── SUBMISSION_CHECKLIST.md          (learners)
├── REFLECTION_QUESTIONS.md          (learners)
├── learner_setup/                   setup guides (learners)
├── data_learners/                   the four team data folders (learners)
├── starter_repo/                    the GitHub repository template (learners)
├── code/
│   └── generate_team_data.py        regenerates the dummy data (instructor)
└── instructor/                      answer key and notes (instructor only, do not share)
```

## For instructors

- Regenerate the data at any time with `python code/generate_team_data.py data_learners`. The seed is fixed, so the data and the answer key stay the same.
- Do not share the `instructor/` folder with learners. Remove it from any zip you give them.
- Before you share the kit, check that `data_learners/` contains only dummy data, and that no `.env` file or secret has been added.

## Important rules for learners (summary)

1. Use only the dummy data. Never upload real client data.
2. Mask customer emails before any AI tool sees them.
3. The AI helpers must never approve, pay, change an invoice or message a customer on their own.
4. The reflection section is typed by hand, with no AI.
