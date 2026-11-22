# Reflection: compulsory, typed by hand, no AI

**Save your answers in `REFLECTION.md` in your repository.**

---

## The rule for this section

You must write every answer in this section **yourself, without any AI tool**. This includes:

- Writing the answer from scratch, in your own words
- Asking an AI to fix spelling, grammar, structure or length
- Asking an AI to explain the topic so you can then write it
- Copying from an AI chat, a website, a book or another learner

You may use your own notes, your code, your data model and your repository, because those are your own work.

**Your trainer may ask you to explain any answer live, face to face or on a call.** If you cannot explain your own answer, the section will be marked down.

**Declaration:** at the top of `REFLECTION.md`, write this sentence and put your name under it:

> "I wrote every answer in this section myself, without AI tools, from my own understanding."

---

## Part 1: The tools you chose (about 200 words)

1. Which tools did you use for the database, the data model, the AI helpers and the cloud? Why did you choose each one?
2. How did each tool work for you? Be specific: what went smoothly, and where did you get stuck?
3. Name three issues you ran into with your chosen tools, and how you solved (or did not solve) each one.
4. If you could start again, what would you change about your tool choices? Why?

---

## Part 2: Problem, architecture and AI system design (about 500 words)

Explain these in your own words. Use plain language. A diagram is welcome, but you must describe it in writing as well.

### 2a. Problem statement (about 100 words)

- What is the client's problem, in your own words?
- Who is affected, and how much does it cost them (in time, money or reputation)?
- Why does the problem exist? Which missing piece causes it?

### 2b. Architecture (about 200 words)

- Describe how the data moves, from the four team systems to your final answer. Name each layer, table or file.
- Explain why the teams keep their own data. What does your design do about that?
- Where are the keys? Describe how you link the order, the delivery, the invoice and the return, and how you handle the problems in the data (for example, the two order number formats and the missing customer key).
- Explain your choice of model shape. Why normalized in one place, and a star schema in another?

### 2c. AI system design (about 200 words)

- Which helpers did you build? For each one: what does it read, what does it decide, and what does it produce?
- Which parts of the decision are code, and which parts (if any) are AI? Why did you split them that way?
- Where does a human step in? What exactly does the person approve?
- How do you protect personal data (customer emails)?
- How do you record what the helpers did? Give an example of one log entry.
- What could go wrong with your design, and how would you find out?

---

## Part 3: Difficulties you faced (about 150 words)

Describe the three hardest difficulties you faced during the assignment. For each one:
- What happened?
- What did you try?
- What did you learn, or what would you do differently?

Be honest. A clear account of a real difficulty is valued more than a polished story with no problems.

---

## Marking for this section

| Part | Points | What we look for |
|---|---|---|
| Part 1: tools and issues | 2 | Specific, honest, based on real use |
| Part 2a: problem statement | 1 | Clear, cost-aware, correct cause |
| Part 2b: architecture | 2 | Matches your repository, explains the keys and the split |
| Part 2c: AI system design | 2 | Clear split between code and AI, human step, privacy, log |
| Part 3: difficulties | 1 | Specific and honest |
| Writing matches your work | 2 | Consistent with your code and diagrams |
| **Total** | **10** | Matches the reflection line in the assignment brief |

**Note:** if the writing style changes sharply between answers, or the answers do not match your repository, your trainer may ask you to explain them live. This check is part of the marking.
