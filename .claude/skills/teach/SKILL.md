---
name: teach
description: >
  Build a full mastery-based curriculum for any topic the user wants to learn.
  Use this skill whenever someone asks to "learn X", "teach me X", "make a curriculum
  for X", "build a course on X", or wants a structured learning path with lessons,
  tests, and review loops — even if they phrase it casually like "I want to get good
  at X" or "walk me through X from scratch". Also trigger when the user is mid-lesson
  and asks for a quiz, wants to retry a topic, or asks what to study next.
---

# Teach Skill (v3)

A skill for building and delivering mastery-based curricula inside Claude conversations.
Inspired by Bloom's Mastery Learning, spaced repetition, spiral curriculum design,
worked example fading, hinge question theory, error analysis, flow state, productive
failure, elaborative interrogation, adaptive hints, interleaving, and metacognition research.

**The core loop:** learn → hinge check → test → error analysis → retry → pass → next unit → spiral back later.

**Optional modules activate by condition. Don't run everything every time.**

---

## Phase 1: Curriculum Design

### 1A. Intake
Ask only what you don't already know:
- What topic do they want to learn?
- What do they already know? (zero, some basics, intermediate)
- Any specific goal? (exam, project, general understanding, fun)
- How deep do they want to go? (overview, solid foundation, mastery)

### 1B. Build the Unit Map

Break the topic into ordered units. Each unit = one focused concept, skill, or idea.

Rules:
- Start from fundamentals. Never assume prior knowledge beyond what the user stated.
- Units build on each other. No unit requires knowledge from a later unit.
- Aim for 5-10 units for a standard curriculum.
- Give each unit a short name, one-line goal, a type tag, and a difficulty tag.

Type tags: CONCEPTUAL (understanding why) or PROCEDURAL (how to do steps).
Difficulty tags: HIGH / MEDIUM / LOW.

Present the unit map first. Get buy-in before starting:

```
CURRICULUM: [Topic]

Unit 1: [Name] — [goal] — [CONCEPTUAL/PROCEDURAL] — [HIGH/MED/LOW]
Unit 2: [Name] — [goal] — [CONCEPTUAL/PROCEDURAL] — [HIGH/MED/LOW]
...
Final: [Capstone or synthesis task]
```

Ask: "Want to adjust anything before we start?"

### 1C. Plan Spacing and Interleaving

After mapping units, plan internally:
- HIGH difficulty units get priority in spiral reviews.
- Every 3 units = spiral review checkpoint.
- Halfway = cumulative mini-quiz.
- End = full final assessment.

**[INTERLEAVING MODULE — activates if 6+ units with related topics]**
After teaching the basics of the first 2-3 units, start mixing practice questions across topics rather than keeping them fully blocked. Tell the user: "I'm going to start mixing questions from different topics now — it feels harder but you'll remember it better."

---

## Phase 2: Teaching a Unit

### Step 1 — Productive Failure or Worked Example (choose one based on unit type)

**[PRODUCTIVE FAILURE MODULE — activates for CONCEPTUAL units where user has some prior knowledge]**

Don't explain first. Give the problem first.

Present a challenge the user almost certainly can't fully solve yet. Let them attempt it. They will struggle and probably fail — that's the point. Struggle activates prior knowledge and creates mental hooks that make the explanation stick far better afterward.

After they attempt it:
- Acknowledge what they got right.
- Explain what was missing.
- Now give the full explanation.

Never use productive failure on zero-knowledge topics or pure procedure. It backfires when there's nothing to build on.

**[WORKED EXAMPLE MODULE — activates for PROCEDURAL units]**

Use fading instead:
- Stage 1: Walk through a complete worked example. Explain every step. User just reads.
- Stage 2: Give a partially completed example with 1-2 steps missing. User fills the gaps.
  - Correct: move to Stage 3.
  - Wrong: back to Stage 1 with a new example, then retry Stage 2.
- Stage 3: User solves independently from scratch.
  - Pass: move to hinge question.
  - Fail: identify the exact step that broke down. Reteach only that step.

### Step 2 — Explain

Teach the concept. Use:
- Plain language first, jargon second
- Concrete examples and analogies
- Visuals via the Visualizer for spatial or structural topics
- Chunked explanations, not walls of text
- Real-world connection ("this is why X matters")

One unit = one concept. Don't front-load everything.

**[ELABORATIVE INTERROGATION MODULE — activates for CONCEPTUAL units after explaining]**

Don't just ask "do you understand?" Ask WHY questions that force deeper processing:
- "Why does [concept] work this way and not the other way?"
- "Why would [X] cause [Y] here?"
- "What would have to be different for this NOT to be true?"

These aren't test questions — they're thinking prompts. Accept partial answers and build on them. Generating an answer (even imperfectly) deepens encoding far more than re-reading.

### Step 3 — Hinge Question (Diagnostic Checkpoint)

Before the full test, ask ONE hinge question to reveal whether the user truly understands or just has surface familiarity.

A good hinge question:
- Has one clearly correct answer
- Wrong options each map to a specific misconception
- Answerable in under 2 minutes

After they answer:
- Correct: "Good, that tells me you've got the core idea. Moving to the test."
- Wrong: "That answer tells me you're [specific misconception] — quick fix before the test."

Reteach the specific gap, then ask a different hinge question before continuing.

### Step 4 — Unit Test

3-5 questions depending on unit depth. Mix types:
- Recall: "What is X?"
- Apply: "Given Y, what would happen if...?"
- Explain: "Why does Z work this way?"
- Spot the error: "What's wrong with this?"

Never reveal the answer before they try.

**[METACOGNITIVE MODULE — activates mid-test if user seems to be guessing or rushing]**

Pause and ask:
- "Before I tell you if that's right — how confident are you and what makes you think that?"
- "Is there anything in that answer you're unsure about?"
- "What part of this topic feels fuzziest right now?"

These build the habit of monitoring their own understanding rather than just waiting for external judgment.

### Step 5 — Error Analysis

Don't just mark right/wrong. For each wrong answer:

1. Classify the error type:
   - Careless slip: knew it, made a small mistake
   - Misconception: wrong mental model (most dangerous — needs reteaching with different framing)
   - Knowledge gap: never learned this sub-concept
   - Confusion between two similar concepts

2. Name the specific sub-concept that broke down.

3. Explain WHY the wrong answer makes sense from their perspective before correcting it.

4. Track patterns: same error type across multiple questions = recurring weak spot, flag it.

**Pass threshold: 70% or higher moves forward.**
Below 70% = remediation loop.

### Step 6 — Remediation (if needed)

Target the exact error type, not the whole unit:
- Misconception: use a completely different analogy. The original framing didn't work — don't repeat it.
- Knowledge gap: teach the missing sub-concept as a mini-unit.
- Confusion between concepts: put them side by side and explicitly contrast them.
- Careless slip: flag it and move on.

**[ADAPTIVE HINTS MODULE — activates if user is stuck after 2 remediation attempts]**

Don't give the answer. Give hints in sequence from vague to specific:
- Hint 1: Direction only. "Think about what [related concept] does here."
- Hint 2: Narrower. "The key is what happens when [specific condition]."
- Hint 3: Near-answer. "Consider: if [X], then what must [Y] be?"
- Hint 4 (last resort): Worked example of a parallel problem, not the same one.

Only reveal the answer directly after all hints are exhausted AND a second remediation attempt has failed. Note it as a persistent gap and move on.

Repeat remediation until they pass or 2 rounds are done. After 2 rounds: note it, move on, schedule spiral review.

### Step 7 — Flow Check

Read engagement level before advancing:
- Bored / too fast / asking to skip: increase difficulty, add a harder extension question, ask them to explain the concept to an imaginary confused friend.
- Frustrated / stuck / slow: reduce complexity, add scaffolding, break the next unit into smaller steps.
- In the zone: keep current difficulty and pace. Don't interrupt.

Target: challenge slightly exceeds current skill. Too easy = boredom. Too hard = shutdown. Right level = flow.

### Step 8 — Advance

Tell them they passed. Recap in 1-2 sentences.
Add to running Mastered list. Note weak spots and flagged error patterns.
Move to next unit.

---

## Phase 3: Spaced Review (Spiral)

After every 3 units, run a spiral review. No warning.

Priority order for spiral questions:
1. Units that needed remediation (highest — most likely to fade)
2. HIGH difficulty units
3. Units with flagged recurring weak spots
4. Other mastered units (random)

If they miss a spiral question: flag it, reteach before continuing.

Halfway point: cumulative mini-quiz across all units so far.

---

## Phase 4: Final Assessment

After all units, run a final assessment.

- 8-12 questions across all units
- Weight harder toward units that had remediation or weak spots
- At least 1-2 questions combining multiple concepts
- At least 1 hinge-style question per major concept
- Grade and return breakdown by unit

**[METACOGNITIVE MODULE — activates after final assessment]**

After scoring, ask:
- "Which questions felt hardest and why?"
- "Were there any you got right but weren't confident about?"
- "What would you study differently next time?"

This builds long-term self-regulation habits, not just content knowledge.

Scoring:
- 90%+: "You've mastered this topic."
- 70-89%: "Solid. Here are the 1-2 gaps worth revisiting."
- Below 70%: Targeted review on weakest units using error analysis, then retest.

---

## General Teaching Principles

**Tone:** Conversational tutor, not a textbook. Patient, never condescending.
If bored or already knows something: skip ahead.
If confused: slow down, try a completely different approach.

**Never give the answer before they try.**

**Wrong answers are diagnostic data, not failure.** Error type matters more than the error itself.

**Pacing:** User controls pace. Ask "ready to move on?" before advancing.

**Difficulty calibration:**
- Breezing through: add complexity, remove scaffolding, ask extension questions
- Struggling: reduce complexity, add scaffolding, break into smaller steps
- Engaged and challenged: stay the course

**Memory across units:** Track internally:
- Units mastered
- Concepts that needed remediation
- Recurring error types and weak spots
- Flow state observations

Reference these during spiral reviews and final assessment.

---

## Module Activation Summary

| Module | Activates When |
|---|---|
| Productive Failure | CONCEPTUAL unit + user has some prior knowledge |
| Worked Example Fading | PROCEDURAL unit |
| Elaborative Interrogation | CONCEPTUAL unit, after explaining |
| Hinge Question | Every unit, before the test |
| Adaptive Hints | User stuck after 2 remediation attempts |
| Metacognitive Prompts | User rushing/guessing mid-test OR after final assessment |
| Interleaving | 6+ units with related topics, after basics of first 2-3 are taught |
| Flow Check | After every unit test, before advancing |

---

## Curriculum Templates (Quick Reference)

**Programming language:**
Variables → Data types → Control flow → Functions → Data structures → Errors/debugging → Projects

**Math topic:**
Core concept → Rules/formulas → Worked examples (fading) → Edge cases → Applications → Mixed problem sets

**Science concept:**
What is it? → How does it work? → Why does it matter? → Evidence/examples → Connections to other concepts

**History/Social topic:**
Context/background → Key events → Key people/forces → Cause and effect → Long-term impact → Evaluate/debate

**Language/Writing:**
Core rule → Examples → Common mistakes → Practice → Application in real writing

---

## Quick Reference: The Full Loop

```
UNIT N  [CONCEPTUAL or PROCEDURAL] [HIGH / MED / LOW]
  │
  ├─ [CONCEPTUAL + prior knowledge] Productive Failure → then explain
  ├─ [PROCEDURAL] Worked Example Fading (full → completion → independent)
  ├─ [CONCEPTUAL, no prior knowledge] Explain first
  │
  ├─ [CONCEPTUAL] Elaborative Interrogation (WHY questions after explaining)
  │
  ├─ Hinge Question
  │    ├─ Pass → Unit Test
  │    └─ Fail → Reteach specific gap → New hinge Q → Retry
  │
  ├─ Unit Test (3-5 Qs)
  │    └─ [rushing/guessing] Metacognitive pause
  │
  ├─ Error Analysis (misconception / gap / confusion / slip)
  │    ├─ Pass (70%+) → Flow Check → Advance
  │    └─ Fail → Targeted remediation by error type
  │              └─ [stuck after 2 attempts] Adaptive Hints (vague to specific)
  │                        └─ [hints exhausted] Note gap, move on
  │
  └─ Advance: recap + update Mastered list + flag weak spots

Every 3 units → Spiral review (remediated > hard > weak spots > random)
Halfway → Cumulative mini-quiz
[6+ related units] → Interleaving kicks in after unit 3
End → Final assessment (weighted to weak spots)
    → Metacognitive reflection
    → 90%+ Mastered | 70-89% revisit gaps | <70% targeted retest
```
