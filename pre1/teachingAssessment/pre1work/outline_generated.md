# Presentation Outline & Slide Plan
## Article: *Doubly-Bounded Queue for Constrained Online Learning*
### AAAI 2025 | Juncheng Wang, Hong Kong Baptist University

---

## PART 1: PRESENTATION OUTLINE (8 minutes)

---

### Opening (~1 minute) — Hook & Context

**Hook (story/question):**
> "Imagine you're a taxi driver in a busy city. You want to earn as much money as possible, but your car has a fuel budget limit each day — and that limit changes depending on gas prices. You have to make pick-up decisions in real time, without knowing what will happen next. How do you stay profitable *and* never break the fuel budget, even as both the fares and the fuel limit keep changing?"

This is essentially the challenge this paper tackles — but for computer algorithms making millions of decisions per second.

**Brief context:**
- Field: **Artificial Intelligence / Machine Learning** — specifically *online learning*, the science of teaching computers to make smart decisions under uncertainty.
- Why it matters: Every time you see an ad online, every time a data center allocates computing power, or a network routes your video stream — these are online learning problems happening in real time, under constantly shifting rules.

**Transition:**
> "Today I'll walk you through what this paper actually did, why it's a breakthrough, and what I've personally learned from it."

---

### Section 1: Introduction to the Article (~1.5 minutes)

**What is the research about?**

The paper is about **online decision-making under changing rules**. Imagine a computer system that must make a sequence of decisions — like how to allocate power across 100 data centers — without knowing in advance what the electricity prices will be or how many jobs will arrive. This is called *Online Convex Optimization* (OCO).

**The gap / problem being addressed:**

Two things can change over time:
1. The **goal** (what you're trying to minimize — e.g., energy cost)
2. The **rules** (constraints — e.g., "you must serve all arriving jobs")

> Think of it like trying to run a relay race where the track keeps changing shape *and* the finish line keeps moving — and you're penalized for stepping outside the lane.

Existing algorithms could keep up with changes in *either* the goal *or* the rules — but **not both at the same time**. When constraints were fixed, the best algorithms could achieve near-zero constraint violations. But as soon as constraints started changing, the violations shot up — no existing method could keep the violation low *and* stay adaptive to both kinds of change simultaneously.

**Research question:**
> *Can we design an algorithm that adapts to both changing goals and changing constraints, and whose performance smoothly recovers to the best-known results when things stop changing?*

**Presenter notes:**
- Avoid terms like "regret bound", "Lyapunov function" — use the relay race / taxi driver analogy instead.
- Transition phrase: *"So the key challenge was… and here's how the authors tackled it."*

---

### Section 2: Key Findings (~2 minutes)

**What did the researchers find?**

The authors proposed a new algorithm called **COLDQ** — *Constrained Online Learning with Doubly-bounded Queue*.

**The key insight — the "doubly-bounded queue":**

> Previous methods used a kind of "penalty counter" to track how badly the constraints were being violated — imagine a taxi driver keeping a running tally of how many km over budget they are. But this counter could grow without limit, or drop below zero in unhelpful ways.

> COLDQ's innovation: keep the counter **trapped between a floor and a ceiling** — like a meter that can only go between 0 and 100. This tight control means the system never catastrophically violates a rule, even when the rules are changing.

**Finding 1 — Adapts to changing goals:**
When the goal (loss function) changes a lot, the algorithm's performance degrades gracefully. When things stabilize, it automatically recovers to the best known performance. *"The findings reveal that COLDQ keeps pace with the dynamics of the loss."*

**Finding 2 — Adapts to changing constraints:**
For the first time, the hard constraint violation also smoothly recovers to near-zero when constraints stop changing. *"Our data indicates that COLDQ is the first algorithm to keep pace with the dynamics of both loss and constraints simultaneously."*

**Finding 3 — Works without inside knowledge:**
The authors also propose an *expert-tracking* variant: run many versions of COLDQ in parallel (each tuned differently), then combine their decisions. This achieves the same strong guarantees **without needing to know in advance how much things will change** — which is critical for real-world deployment.

**Real-world experiment:**
The algorithm was tested on actual electricity price data from New York City (NYISO, May 2017), scheduling jobs across 100 simulated data centers. COLDQ outperformed state-of-the-art competitors in reducing delayed jobs while keeping energy cost competitive.

**Presenter notes:**
- Use the slide showing the comparison table/figure from the paper.
- Signaling language: *"The analysis demonstrates that…"*, *"We observed noteworthy trends, particularly in…"*
- Pause after each finding for audience to absorb.

---

### Section 3: Significance of the Research (~1.5 minutes)

**Why do these findings matter?**

This paper closes a gap that has existed in the field for years. Before this work, researchers had to choose: either handle changing goals well, *or* handle changing constraints well — not both.

> Think of it as finally inventing a car that is both fuel-efficient *and* fast — where before, you always had to sacrifice one for the other.

**Contribution to the field:**
- *"This research contributes to the field by providing the first algorithm that simultaneously achieves the best-known performance on both fronts."*
- It generalizes cleanly: when changes diminish (either in goals or constraints), COLDQ's performance automatically tightens to match the theoretical best. This "smooth recovery" property is a new standard for constrained online learning.

**Broader implications:**
- **Advertisement placement** — more efficient ad systems that respect budget constraints even as user behavior shifts.
- **Cloud computing / data centers** — smarter power allocation that meets service-level agreements during demand spikes.
- **Network management** — adaptive routing that respects bandwidth limits in dynamic traffic conditions.
- **Any real-time resource management system** where both cost functions and capacity limits fluctuate.

*"By addressing this gap, we advance our understanding of how intelligent systems can operate robustly in the unpredictable real world."*

**Presenter notes:**
- Connect to audience: *"Think about how Netflix decides which server handles your video stream — this is exactly the kind of problem this paper helps solve."*
- Keep it accessible — no equations needed here.

---

### Section 4: Impact on My Own Research (~1.5 minutes)

**How might this paper influence my research design?**

*(Note: Customize this section to your specific research topic. The template below is structured for a student in CS/AI.)*

This paper directly influences how I think about **designing algorithms that must operate under real-world constraints** — constraints that are not static, but shift with time.

Specifically:
1. **The doubly-bounded queue mechanism** is a powerful design pattern: instead of letting a penalty term drift freely, bounding it both above and below gives predictable, controllable behavior. I can apply this principle in [*my own algorithm design for ___*].
2. **The expert-tracking extension** shows me a practical way to handle uncertainty about system parameters — running parallel versions and aggregating is a robust and elegant solution. This is relevant to my work on [*Constraint Online Convex Optimization*] where I also face unknown hyperparameters.

**Good writing skills learned from this article:**

1. **The "key question" technique (Introduction, para. 4):**
The authors end their literature review with a single, bold research question set in italics:
> *"Can a constrained OCO algorithm provide a dynamic regret bound and a constraint violation bound that smoothly approach to the best-known O(T^{1/2}) regret and O(1) violation...?"*
This is extremely effective — it creates suspense, tells the reader exactly what gap is being filled, and sets up the contributions that follow. **I will use this technique** in my own paper writing to crystallize my research question before presenting my contributions.

2. **Structured contributions section:**
The paper lists contributions as bullet points right after the key question, using parallel grammatical structure ("We propose…", "We analyze…", "We show…", "We further propose…"). This makes the paper's value immediately clear. Evidence: *"We summarize our contributions below"* followed by four clean, numbered claims. **I will adopt this pattern** to make my own contributions scannable and persuasive.

3. **Motivating with a smooth-recovery narrative:**
Rather than simply claiming "our algorithm is better," the authors frame the entire paper around the concept of *"smoothly approaching the best-known bounds as dynamics diminish."* This narrative thread runs through introduction, theorems, and experiments consistently. It demonstrates how a single compelling story unifies a complex technical paper.

**Presenter notes:**
- Be personal and specific — give real examples from your own research.
- Use phrase: *"What I found particularly valuable was…"*
- Reference specific lines/sections of the paper as evidence.

---

### Closing (~0.5 minutes)

> "To sum up: this paper tackles a classic but unsolved problem — making smart decisions in real time when both the goals and the rules keep changing. The COLDQ algorithm achieves this by introducing a clever double-bounded tracking mechanism, and for the first time, delivers theoretical guarantees that smoothly recover the best-known performance as the environment stabilizes. Beyond the technical result, I've gained concrete lessons in how experienced researchers structure arguments, frame contributions, and tell a compelling research story."

> "Thank you for your attention. I'd be glad to answer any questions you might have."

**Presenter notes:**
- Maintain eye contact during closing.
- Slow down pace — give the audience time to absorb the summary.
- Smile when inviting questions — approachable body language.

---

## PART 2: SLIDE PLAN

---

### Slide Count: 10 slides (approx. 48 sec/slide average)

---

### Slide 1 — Title Slide
**Title:** Making Smart Decisions Under Changing Rules
**Subtitle:** A Study of *Doubly-Bounded Queue for Constrained Online Learning* (AAAI 2025)
**Content:**
- Your name & student ID
- Date
- Course: MCCP6020

**Visual:** Clean background; optional: animated graph showing a fluctuating curve being "tamed" by a bounded zone
**Design notes:** Minimal text; large font (36pt+ for title); high contrast

---

### Slide 2 — Hook: The Taxi Driver Problem
**Title:** Imagine You're a Taxi Driver…
**Content (bullet points):**
- Must earn income in real time
- Fuel budget changes daily
- No idea what tomorrow holds
- How do you stay profitable AND never overspend?

**Visual:** Simple icon of a taxi + a fuel gauge; or a stylized city map
**Design notes:** Single vivid image; use the question as the only text block

---

### Slide 3 — What is Online Learning?
**Title:** Computers Facing the Same Challenge
**Content:**
- Make decisions *now*, without knowing the future
- Learn from each decision after the fact
- Applied in: ad placement, cloud computing, network routing

**Visual:** Simple flowchart: Decision → Outcome Revealed → Update → Next Decision
**Design notes:** Diagram only; no dense text; 3 icons for applications

---

### Slide 4 — The Unsolved Problem
**Title:** The Gap No One Could Close
**Content:**
- Goal (loss) changes over time ✓ — handled by existing methods
- Rules (constraints) change over time ✗ — NOT handled well
- Best known: constraint violations *explode* as rules change
- **Key question:** Can one algorithm handle BOTH?

**Visual:** Two-column comparison table (Goal dynamics vs. Constraint dynamics); red "✗" for missing combination
**Design notes:** Visual contrast between "solved" and "unsolved" is key; bold the question

---

### Slide 5 — The COLDQ Solution
**Title:** Introducing COLDQ
**Content:**
- C-O-L-D-Q = **C**onstrained **O**nline **L**earning with **D**oubly-bounded **Q**ueue
- Key innovation: a "penalty counter" with both a floor AND a ceiling
- Result: constraint violations stay under control — always

**Visual:** Animated gauge/meter diagram showing a counter bouncing within bounds (vs. an unbounded counter flying off-screen)
**Design notes:** Use color coding — red for unbounded (old), green for bounded (COLDQ)

---

### Slide 6 — Key Finding 1: Adapts to Changing Goals
**Title:** Finding 1 — Keeps Pace with Changing Goals
**Content:**
- When goals change a lot → performance degrades gracefully
- When goals stabilize → performance recovers to theoretical best
- First algorithm to achieve this "smooth recovery" property

**Visual:** Graph sketch: x-axis = "amount of change", y-axis = "performance penalty"; COLDQ curve smoothly slopes to 0
**Design notes:** One graph per slide; annotate key point directly on graph

---

### Slide 7 — Key Finding 2: Adapts to Changing Constraints
**Title:** Finding 2 — Keeps Pace with Changing Rules (First Time Ever)
**Content:**
- Hard constraint violation also "smoothly recovers" to near-zero
- This was **never achieved before**
- No need for restrictive technical assumptions (no Slater condition)

**Visual:** Comparison bar chart — COLDQ vs. competitors for constraint violation
**Design notes:** Highlight COLDQ bar in a distinct color; label clearly

---

### Slide 8 — Real-World Results
**Title:** Tested on Real Data: New York City Power Grids
**Content:**
- 100 virtual data centers, real electricity prices (NYISO, May 2017)
- Goal: minimize energy cost + serve all arriving jobs on time
- COLDQ: fewer delayed jobs than all competitors

**Visual:** Line graph (from paper's experiments) showing accumulated violations over time; COLDQ line lowest
**Design notes:** Use actual figure from paper if possible (simplified/annotated version)

---

### Slide 9 — Why It Matters & Impact on My Research
**Title:** Significance + What I Learned
**Content:**
**Significance:**
- Closes a long-standing gap in online learning theory
- Applicable wherever decisions + rules are both dynamic

**Impact on my research:**
- Design pattern: double-bounding a penalty term for stability
- Writing lesson 1: End lit review with a bold "key question"
- Writing lesson 2: Use parallel structure for contributions

**Visual:** Two-column layout: left = "Broader Significance", right = "Personal Takeaways"
**Design notes:** Keep each column to 3 bullet max; use icons

---

### Slide 10 — Conclusion & Q&A
**Title:** To Sum Up…
**Content:**
- COLDQ = first algorithm to pace with BOTH changing goals AND rules
- Achieved via doubly-bounded queue + new mathematical analysis
- Lessons: structure, framing, and the "key question" technique

**Visual:** Single takeaway sentence in large font; "Thank you / Questions?" at bottom
**Design notes:** Clean, uncluttered; make the Q&A invitation visually prominent

---

## HTML Slide Format Specifications

```
Framework: Reveal.js (lightweight, browser-based, keyboard navigable)
Navigation: Arrow keys + click to advance; overview mode with Esc key
Layout: 16:9 widescreen format
Font: Title 40-44pt, Body 24-28pt, Notes 18pt
Color scheme:
  - Background: #1a1a2e (dark navy)
  - Primary accent: #3498db (blue)
  - Text: #f0f0f0 (off-white)
  - Highlight: #e74c3c (red for emphasis)
Minimal text principle: max 5 bullet points per slide, max 8 words per bullet
All diagrams: SVG or Canvas-drawn (no raster images where avoidable)
Responsive: scales to projector, laptop, and tablet screens
```

---

*Generated by AI Agent on 2026-02-23. Please review for accuracy before use.*
*Next step: Read this outline carefully, then write your feedback in `feedback.md`.*
