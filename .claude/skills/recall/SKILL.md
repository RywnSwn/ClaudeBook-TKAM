---
name: recall
description: >
  Build a deep recall and essay-prep system for any book, text, or subject the user
  needs to memorize and analyze. Use whenever someone says "/recall", "help me memorize
  this book", "I have a test on X", "drill me on X", "I need to remember X for an exam",
  or wants to practice essay writing from memory. Works even when Claude has no prior
  knowledge of the book -- the user is the source of truth. Designed for learners who
  understand through fast conversation, not note-taking.
---

# Recall Skill (v1)

A skill for building deep recall and essay-prep readiness from any book or subject.
Grounded in the testing effect (Roediger & Karpicke, 2006), elaborative interrogation
(Dunlosky et al., 2013), prompted recall over free recall (constructive retrieval hypothesis),
spaced repetition, Feynman technique, and error-pattern tracking.

**The core difference from /teach:** Claude does NOT need to know the content.
The user is the knowledge source. Claude organizes, drills, and deepens from what the
user provides. Fast, accurate, unpolished answers are treated as valid -- grammar and
style are irrelevant, only understanding matters.

**The core loop:** intake conversation → knowledge base → gap fill → recall drills →
Feynman checks → essay mode → weak spot summary → spiral back.

**Weak spot tracker runs through ALL phases.** Every miss, shallow answer, or hesitation
gets logged internally and surfaces at the end of each session as a danger list.

---

## Phase 0: Intake

### 0A. Ask only what you don't know yet

Before drilling anything, ask:
- What's the book/subject/topic?
- What format is the test? (essay, short answer, multiple choice, open book, closed book -- if unknown, say "tell me when you find out and I'll adjust")
- How much time until the test?
- What do you already remember about it? (just start talking, doesn't have to be organized)

Keep this conversational. Don't ask for notes. Don't ask them to write anything structured.
Fire short questions, let them answer fast and messy.

### 0B. Build the Knowledge Base

As the user talks, Claude organizes internally into:

**Characters** -- name, role, key traits, arc, relationships, key moments
**Themes** -- what the book is actually about beneath the plot
**Plot structure** -- key events per chapter/act in order
**Key quotes** -- any the user remembers, with context and why they matter
**Author's techniques** -- any literary devices, style choices, recurring symbols
**Gaps** -- anything that came up thin or uncertain

After intake, show the knowledge base to the user in a compact format:

```
KNOWLEDGE BASE: [Book Title]

CHARACTERS:
[Name] -- [role] -- [key trait] -- [arc in one line]
...

THEMES:
[Theme] -- [how it shows up in the book]
...

KEY PLOT POINTS:
[Chapter/Act] -- [what happens] -- [why it matters]
...

QUOTES REMEMBERED:
"[quote]" -- [who/when] -- [why it matters]
...

GAPS (thin or uncertain):
- [topic]
...
```

Ask: "Does this look right? Anything wrong or missing?"
Let them correct it. Update the base. Then move to Phase 1.

---

## Phase 1: Gap Filling

Before drilling, close the gaps identified in Phase 0.

For each gap, ask targeted questions to pull out what they know:
- "You mentioned [character] but weren't sure about their arc -- what do you remember happening to them by the end?"
- "You said [theme] but what's a specific moment in the book that shows that?"

Rules:
- Never lecture. Ask, don't tell.
- If they genuinely don't know something, note it in the weak spot tracker as a KNOWLEDGE GAP and move on. Don't invent content.
- If the book is unknown to Claude, say so upfront: "I don't have this book in my training -- everything I test you on will come from what you tell me, so be as detailed as you can."

**WEAK SPOT TRACKER -- activates here:**
Log every gap that can't be filled. Flag it as a priority in Phase 2 drills.

---

## Phase 2: Recall Drills

The core engine. Pure retrieval practice -- the testing effect in action.

### Drill Types (mix these, never block one type for too long)

**Fact recall** -- "What does [character] do in chapter [X]?"
**Relationship recall** -- "How does [character A] feel about [character B] and why?"
**Quote recall** -- "Do you remember any quote that shows [theme/trait]? Rough is fine."
**Cause and effect** -- "What causes [event] and what does it lead to?"
**Sequence** -- "What order do these three events happen in: [A], [B], [C]?"
**Contrast** -- "How is [character A] different from [character B]?"

### Rules

- Never give the answer before they try.
- Fast, accurate, unpolished answers are correct. Don't penalize grammar or style.
- Wrong or uncertain answers: classify the error before moving on (see error types below).
- After every 5-6 drills, check: are they breezing through or struggling?
  - Breezing: go harder, ask for more specific details or edge cases
  - Struggling: slow down, ask simpler version of the same question first
  - In flow: keep going

### Error Types (classify every miss)

- **Knowledge gap** -- never learned this detail, truly doesn't know
- **Confusion** -- mixed up two characters, events, or concepts
- **Decay** -- knew it before, forgotten now (most important for spaced review)
- **Surface only** -- got the fact right but can't explain why it matters

**WEAK SPOT TRACKER -- active throughout:**
Every error type gets logged with the specific concept. Same error type appearing
twice = recurring weak spot, flag it for spiral review priority.

---

## Phase 3: Feynman Checks

After every 8-10 drills, switch from fact recall to explanation mode.

Don't ask "do you understand?" Ask them to explain:

**Character check:** "Explain [character]'s whole arc to me like I've never read the book -- just talk."
**Theme check:** "Why is [theme] the central idea of this book? What in the story makes you say that?"
**Motivation check:** "Why does [character] make [specific decision]? What does that tell us about them?"
**Author check:** "Why do you think the author wrote [scene/event] the way they did?"

### Evaluating Feynman answers

Claude checks the explanation against the knowledge base (not its own knowledge).

- **Deep:** they connected the idea to other parts of the book, explained the why not just the what -- pass
- **Surface:** they described what happened but not why it matters -- probe deeper with one follow-up "why" question
- **Wrong:** contradicts something in the knowledge base -- classify as confusion or knowledge gap, add to weak spot tracker

**[ELABORATIVE INTERROGATION MODULE -- always on during Feynman checks]**

After any Feynman check, ask one "why" or "how" follow-up regardless of how good the answer was:
- "Why does that matter for the theme?"
- "How does that change how you'd read the ending?"
- "Why do you think the author made that choice specifically?"

These build retrieval hooks -- the more connections, the easier recall under exam pressure.

**WEAK SPOT TRACKER -- active here:**
Surface-only or wrong Feynman answers get flagged as DEEP UNDERSTANDING gaps,
separate from fact gaps. Both types need different remediation.

---

## Phase 4: Essay Mode

Activate when:
- User asks for it
- User mentions an essay component to the test
- The knowledge base is solid enough (Phases 2-3 mostly passed)

### 4A. Ask about test format first (if not already known)

"What do you know about the essay format? Like is it a prompt they give you beforehand, a surprise prompt, a specific character or theme, or totally open?"

Adjust based on what they say.

### 4B. Give a practice prompt

Generate a realistic essay prompt based on the book's themes and characters.
Example formats:
- "How does [theme] develop through [character]'s journey? Use specific evidence."
- "What does [character]'s arc reveal about [theme]?"
- "Compare how [character A] and [character B] respond to [conflict]. What does this say about [theme]?"

### 4C. Mini essay response drill

Don't ask them to write a full essay. Ask them to:

1. State their thesis in one sentence
2. Name 2-3 pieces of evidence they'd use (quotes or specific moments)
3. Explain how each piece connects to the thesis

This is a verbal/fast version. Accept messy, accurate answers.

### 4D. Evaluate the response

Check against knowledge base:
- Is the thesis arguable (not just a fact)?
- Is the evidence specific and relevant?
- Does the explanation connect evidence to the claim, not just describe what happened?

**[QUOTE BANK CHECK -- activates if quotes are thin]**
If they can't recall specific quotes, run a targeted quote drill:
- "Do you remember anything [character] said about [theme]?"
- "Is there a moment in chapter [X] you could quote or paraphrase?"
Rough paraphrases count -- exact wording matters less than knowing the moment exists.

**WEAK SPOT TRACKER -- active here:**
Log: weak thesis construction, poor evidence selection, description instead of analysis.
These are essay-specific weak spots, tracked separately.

---

## Phase 5: Session Wrap -- Weak Spot Summary

At the end of every session, surface the tracker:

```
SESSION WEAK SPOTS

KNOWLEDGE GAPS (didn't know):
- [specific topic/detail]

CONFUSION ERRORS (mixed up):
- [what got confused with what]

DECAY ERRORS (forgot, used to know):
- [topic] -- priority for next session

DEEP UNDERSTANDING GAPS (surface only):
- [concept] -- needs more why/how drilling

ESSAY WEAK SPOTS:
- [thesis/evidence/analysis issue]

PRIORITY FOR NEXT SESSION:
1. [highest priority item]
2. [second]
3. [third]
```

Ask: "Want to drill any of these right now before we stop?"

---

## Phase 6: Spaced Spiral Review

At the start of every new session on the same book, before anything else:

Pull from the previous session's weak spot list. Start with decay errors (most likely to have faded), then knowledge gaps, then deep understanding gaps.

Don't announce this as a review -- just start drilling the weak spots naturally.
If they get them right: "Good, that one's solid now."
If they miss again: reteach by asking them to make the connection themselves, not by telling them.

**Spaced timing (if user mentions they have X days):**
- Day 1: full intake + phases 1-3
- Day 2-3: spiral weak spots + essay mode
- Day before test: fast-fire weak spot drill only, no new content

---

## Module Activation Summary

| Module | Activates When |
|---|---|
| Knowledge Base Display | After intake, every time |
| Gap Filling | Gaps identified in intake |
| Recall Drills | Phase 2, always |
| Feynman Checks | Every 8-10 drills |
| Elaborative Interrogation | Every Feynman check, always |
| Quote Bank Check | Essay mode + quotes are thin |
| Essay Mode | User requests it OR test has essay component |
| Weak Spot Tracker | ALL phases, always running |
| Spaced Spiral | Start of every new session on same book |

---

## General Principles

**Claude does not know the book.** The user is the source of truth. Never invent
plot points, quotes, or character details. If unsure, ask.

**Fast, accurate, unpolished = valid.** Never penalize grammar, formatting, or
sentence structure. Only check for correctness of understanding.

**Wrong answers are diagnostic data.** Error type matters more than the error itself.
Classify before responding.

**Never give the answer before they try.** If they're stuck, ask a simpler version
of the same question first.

**Depth over breadth.** 10 things understood deeply beats 50 things memorized shallowly.
Prioritize the Feynman checks as much as the fact drills.

**Adaptable format.** If user tells you the test format, adjust:
- Closed book essay: weight heavily toward quote recall and essay mode
- Short answer: weight toward fact recall and cause/effect drills
- Multiple choice: add contrast drills and confusion-type error prevention
- Unknown: cover all bases, ask user to update when they find out

**Weak spots come back.** Anything flagged in the tracker returns in the next session.
Mastery means getting it right twice across separate sessions, not just once.
