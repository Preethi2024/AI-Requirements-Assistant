# AI Requirements Assistant

**▶ [Try the tool](https://claude.ai/artifact/JEDkMRehuX6XyfudHWK92U)** — three sample transcripts are built in, nothing to set up.

A tool that turns raw meeting notes into draft user stories with acceptance criteria, and flags the requirements that cannot be tested as written.

---

## The problem

After a requirements workshop you have two hours of messy notes and a backlog to write. Two things take the time.

**Typing up the stories** is mechanical and slow, and it's the part that gets rushed at 7pm — which is when acceptance criteria quietly shrink to a happy path only.

**Spotting what was never actually agreed** is the harder one. Someone said "it should be fast", "handle it gracefully", "a reasonable number", "we'll deal with that later". Those phrases pass unchallenged in the room and reappear as disputes in UAT, when the cost of resolving them is highest.

The second problem is the one this tool is built around. Draft stories save typing. Knowing which sentence in a meeting was never settled is the job.

---

## How it works

The notes go to an LLM with an instruction set that encodes what a well-formed requirement looks like. That instruction set is the analysis work — the model supplies the language, the rules supply the judgement.

| # | Rule | Why |
|---|---|---|
| 1 | One testable behaviour per story; split anything containing two | "Save the card and show the bank logo" is two pieces of work with two tests. Merged stories are the commonest reason a story rolls into the next sprint |
| 2 | Minimum three acceptance criteria — happy path, edge case, negative case | Happy-path-only stories are where UAT defects come from |
| 3 | Criteria describe observable behaviour, never implementation | "Then the token refreshes" is something QA can't see; "then the user stays logged in" is |
| 4 | "Won't" priority only where the notes explicitly defer something | Stops the tool inventing scope decisions nobody made |
| 5 | Flag every unquantified phrase, quoting the words actually used, with the question to ask and who should answer it | The core of the tool |
| 6 | Never generate a requirement the notes don't support | An invented requirement is worse than a missed one, because nobody reviews it |

Output is a first draft for a human to edit — never a finished backlog. A tool claiming otherwise is making a claim no analyst should accept.

---

## What it produces

From a 20-line sprint-planning transcript about saving card details at checkout:

- **7 review-ready draft stories**, each with role, capability, outcome, MoSCoW priority and Given/When/Then criteria
- **Ambiguity flags** quoting the transcript directly — "should be pretty fast", "a reasonable number", "handle that gracefully" — each with the clarification question to take back
- **Open questions and assumptions** the meeting left unresolved
- **Markdown export**, so the output goes straight into Jira or a requirements doc

Three transcripts are built in — sprint planning, client discovery, support escalation — each written to contain specific traps: unquantified language, a requirement nobody pinned down, an explicit deferral, and an unstated impact.

---

## Limitations

Worth stating plainly, because they're real:

- It can only work from what's in the notes, so it inherits whatever the note-taker missed
- It doesn't know an organisation's conventions, naming, or existing backlog
- It reproduces vagueness it fails to recognise — the flagging is good, not complete
- The output always needs editing; the saving is in the first draft, not the final one

---

## Built with

Claude (for generation), HTML/JS for the interface. The requirement-quality rules and the test transcripts are mine.

---

**G P Preethi** · Business Analyst · Bengaluru
[LinkedIn](https://linkedin.com/in/g-p-preethi) · gppreethim@gmail.com
