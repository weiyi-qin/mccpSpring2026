# Design and story notes for the 3MT one-slide submission

This document explains how the one-slide visual was designed and how the research story is presented to a non-specialist audience.

## 1. Research topic used for this 3MT slide

- Topic: Double-Q for constrained online convex optimization
- Core idea in plain English: making good online decisions when the rules can change after each decision is made
- Main public-facing message: one method can help a system keep moving efficiently without breaking too many important rules

## 2. Why I chose this slide design

The 3MT brief requires one static slide for a non-specialist audience, so I did not turn the research into a dense technical slide. Instead, I used one dominant visual metaphor: **driving with changing road rules**.

This metaphor supports the main research story:

- Online decision-making becomes a driver moving step by step
- Time-varying constraints become changing road rules or traffic signals
- Hard constraint violation becomes running a red light, which cannot be undone later
- Double-Q becomes a two-signal dashboard that watches both progress and safety

I chose this design because it is easier for a lay audience to understand than abstract mathematical terms such as regret, constraint variation, or virtual queues.

## 3. Main visual choices

### Hook-based title

The title is phrased as a question:

- `What if your GPS had to drive before today's road rules were posted?`

This is intended to work as an attention-getter and to quickly place the audience inside an everyday situation.

### One central metaphor

The center of the slide is a road with changing traffic lights and a central Double-Q control hub. This gives the audience one image to remember, rather than several disconnected charts or equations.

### Minimal text

The slide uses short text blocks only:

- one block for the challenge
- one block for the core idea
- one bottom impact statement

This keeps the slide readable and leaves space for the spoken explanation.

### Color coding

- Warm orange is used for risk, alerts, and changing conditions
- Deep teal is used for control, safety, and the proposed method
- Light cream is used for readability and visual calm

This makes the slide easier to follow without requiring technical labels.

## 4. How I explain the research story to a non-specialist audience

I plan to explain the story in five simple moves.

### Move 1: Opening hook

I begin with the GPS-and-road-rules scenario. This creates a familiar situation before I mention my actual field.

### Move 2: Why the problem matters

I explain that many real systems must act before they know all the current rules. I use examples such as scheduling, resource allocation, and fraud detection.

### Move 3: What makes the problem hard

I explain that some mistakes are not reversible. Instead of using the term "hard constraint violation" first, I explain it as "running a red light that cannot be cancelled later."

### Move 4: What my research does

I introduce Double-Q as a two-warning system:

- one signal watches progress
- one signal watches risk

This lets me mention the method briefly without turning the talk into a technical lecture.

### Move 5: Why it matters

I end with the significance:

- more reliable decisions under changing conditions
- fewer costly or unsafe rule-breaking decisions
- better support for practical systems that must operate online

## 5. 3MT strategies used

The slide and story use several 3MT-friendly strategies recommended in the course materials:

- a question-based opening hook
- a daily-life metaphor
- plain language instead of jargon
- one static visual with a clear focal point
- emphasis on significance and applications rather than detailed methodology

## 6. Alignment with the assignment requirements

| Requirement | How this submission addresses it |
| --- | --- |
| One-page slide in a machine-readable format | The slide is a text-based HTML file with editable text and SVG shapes. |
| Suitable for a non-specialist audience | The slide uses a driving metaphor, short labels, and avoids technical terminology on the slide itself. |
| Explain aims, results, and/or significance | The spoken story supported by the slide focuses on the problem, the proposed idea, and why it matters. |
| Short markdown file describing design and story | This file documents both the slide design choices and the storytelling strategy. |

## 7. What still needs to be customized

- Replace `[Your Name]` on the slide
- Add the final audio link after recording
- Adjust any wording if the spoken version changes during rehearsal
