---
name: paper-deep-read
description: Use when the user wants to deeply read, explain, learn, or interpret an English technical paper or a specific section, equation, sentence, term, method, experiment, or claim. Preserve the paper's technical meaning, explain difficult content in simpler English first, then use Chinese to verify and deepen understanding. Separate paper claims from interpretation, inference, and project transfer.
---

# Paper Deep Read

## Core principle

Help the user understand technical papers increasingly through English rather than through translation alone

The default learning path is

```text
Original paper
    ↓
Paper idea / paper-style English
    ↓
Plain English
    ↓
Technical vocabulary and sentence logic
    ↓
Equation / method interpretation
    ↓
中文深解
    ↓
Research or project connection when useful
```

The goal is not to replace the paper with a Chinese summary

The goal is to make difficult technical English understandable while preserving the original technical claim

## Scope boundary

This skill is for deep reading after a paper or paper section has been identified

It may explain

- abstract and introduction
- method and architecture
- equations and symbols
- experiments and ablations
- discussion and limitations
- difficult sentences
- technical terminology
- claims and assumptions
- connections to existing robotics, control, learning, or engineering knowledge
- possible research or project transfer when grounded in the paper

This skill is not a paper scouting or daily literature-digest workflow

Do not turn the task into broad literature search, venue ranking, impact-factor comparison, or daily recommendation unless the user explicitly asks for those things

If the user later decides to reproduce or implement a concrete idea, hand the engineering planning task to `mini-step-plan` when available

## 1 Source-first reading

Read the strongest available source before explaining technical details

Prefer this evidence order

```text
1 paper body
2 supplementary material
3 official project page
4 official source code
5 publisher or proceedings metadata
6 author-provided material
7 secondary explanation
```

Never substitute a secondary summary for the original paper when the original paper is available

For method, experiment, equation, limitation, and numerical-result claims, prefer the paper body or supplementary material

If the paper itself is unavailable or incomplete, state the evidence limitation and avoid presenting reconstructed details as confirmed paper content

Do not invent missing equations, results, implementation details, publication venues, code availability, or author intent

## 2 Choose the minimum useful reading mode

Infer the mode from the user's request whenever possible

### QUICK

Use when the user wants to know what the paper is about or whether it is worth deeper reading

Focus on

- problem
- core idea
- method map
- main evidence
- why it matters

Do not expand into a full section-by-section lecture

### SECTION

Use when the user asks for one section such as Introduction, Method, Experiments, or Discussion

Stay inside that section except for the minimum context needed to explain it

### DEEP

Use when the user asks for a complete deep reading

Typical order

```text
Abstract
Introduction
Required background concepts
Method
Equations
Experiments
Discussion
Limitations
Research connection
```

Do not force every section to have equal length

Spend detail where the technical difficulty or importance actually is

### TARGETED

Use when the user asks about one sentence, term, equation, figure, claim, or concept

Answer that target directly

Do not restart the whole paper unless the missing context is necessary

## 3 English-first explanation

Default to roughly 55 to 65 percent English and 35 to 45 percent Chinese when the user has not specified another ratio

The ratio is directional rather than a strict word count

English and Chinese have different jobs

### English should primarily explain

- what the paper claims
- what problem is being solved
- how the method works
- why the design makes sense
- what a technical term means in this paper
- how a difficult sentence is logically constructed

### Chinese should primarily explain

- the underlying technical intuition
- why the authors chose this design
- mathematical or control-theoretic meaning
- connections to the user's existing knowledge
- likely misunderstandings
- implications for research or engineering practice

Avoid simply duplicating the same paragraph in two languages

## 4 Three-layer explanation contract

For important technical ideas, use this order when useful

### Paper idea

Give a faithful paper-style paraphrase in English

Preserve the scope and technical meaning of the original statement

Do not make the claim stronger than the paper

### Plain English

Rewrite the idea using simpler English without removing the important technical structure

Prefer short causal explanations, concrete examples, and explicit subject-verb relationships

### 中文深解

Explain the underlying concept in Chinese

Focus on why the idea works, how it relates to robotics or engineering concepts, and what a Chinese native speaker is most likely to misread

Do not make the Chinese section merely a translation of the Plain English section

## 5 Claim separation

Keep four categories distinct

### Paper claim

A statement the paper explicitly makes or directly supports with its method, theory, or experiment

### Interpretation

An explanation used to make the paper easier to understand

### Inference

A conclusion that follows reasonably from the paper but is not itself stated as a paper claim

### Project connection

A possible transfer to another system, project, or research direction

Never present an inference or project connection as though the authors demonstrated it

Use clear wording such as

- `The paper shows ...`
- `A useful way to interpret this is ...`
- `This suggests ...`
- `For your project, a possible adaptation would be ...`

When uncertainty matters, state it explicitly

## 6 Technical vocabulary contract

Do not create a generic bilingual word list

Select only terms that carry important technical meaning in the current paper

For each important term, explain as needed

```text
Term
↓
Meaning in this paper
↓
Plain-English definition
↓
中文概念
↓
Why this wording matters
↓
Common misunderstanding
```

Prefer phrases such as

- structured action representation
- contact-consistent equilibrium
- demonstration manifold
- direction-dependent stiffness
- motion field
- latent dynamics

rather than isolated basic words unless the user specifically asks about them

When a common English word has a specialized technical meaning, explain the difference

Examples include

- representation
- consistent
- manifold
- nominal
- residual
- compliance
- policy
- rollout

## 7 Sentence Clinic

Use `Sentence Clinic` selectively for sentences whose grammar or logical structure blocks understanding

Break down only what is useful

Possible structure

```text
Original or faithful paraphrase

Main subject
Main verb
Main complement
Important modifier
Logical connector
Technical meaning

Plain English rewrite
```

Explain why a phrase such as `consistent with`, `subject to`, `conditioned on`, or `in contrast to` matters when that wording changes the technical interpretation

Do not turn every sentence into a grammar exercise

## 8 Equation and symbol explanation

Do not merely translate the symbols

For an important equation explain as needed

1. what physical or mathematical quantity the equation expresses
2. what each symbol means in the paper
3. what changes when a variable increases, decreases, or becomes zero
4. what assumptions are implicit
5. how the equation connects to the method
6. one simple numerical or physical intuition when helpful

Separate exact paper definitions from your own intuition

If an equation is not visible in the available source, do not reconstruct it from memory as though it were quoted from the paper

## 9 Figure and architecture explanation

When a figure or architecture is important, explain the information flow rather than only naming boxes

Prefer a structure such as

```text
Input
  ↓
Representation
  ↓
Learned module
  ↓
Physical or algorithmic constraint
  ↓
Controller / decoder / estimator
  ↓
Output
```

Then explain

- what information enters each stage
- what transformation occurs
- what is learned
- what is hand-designed
- where physical constraints enter
- what the output means operationally

## 10 Experiment reading

For experiments, separate four questions

```text
What hypothesis is being tested
What baseline is used
What metric is measured
What conclusion is actually supported
```

Do not equate a better reported metric with proof of every claimed advantage

For sim-to-real or real-robot results, distinguish

- simulation evidence
- hardware evidence
- number and diversity of tasks
- number of trials when reported
- success metric
- failure cases or limitations

Ablations should be explained as evidence about components, not as a generic performance table

## 11 Research and project connection

Only add a connection when it is useful and technically grounded

Default to at most three meaningful connections

Classify each connection as one of

### Directly reusable

The paper's method or component can be reused with relatively small changes

### Adaptable

The core idea transfers, but the representation, controller, data, hardware, or assumptions need meaningful changes

### Research inspiration

The paper suggests a new question or hypothesis but does not directly provide a reusable solution

Be explicit about what comes from the paper and what is newly proposed for the user's project

Avoid generic statements such as `this is very suitable for your project` without explaining the actual technical bridge

## 12 Reproduction boundary

A deep reading may identify a minimal reproduction idea, but do not automatically turn the explanation into a large implementation plan

A useful end state is

```text
Paper idea
    ↓
What would need to be reproduced
    ↓
Minimal research hypothesis
    ↓
Possible experiment
```

If the user asks to implement, reproduce, or integrate it, use `mini-step-plan` when available and keep the paper explanation as context rather than mixing the two workflows

## 13 Output template

Use `READING_TEMPLATE.md` as a guide rather than a rigid form

Skip sections that add no value

For TARGETED mode, answer the target directly and use only the relevant subset of the template

For DEEP mode, use repeated local cycles of

```text
Paper idea
Plain English
中文深解
```

rather than placing all English first and all Chinese at the end

## Quality gate

Before returning the explanation verify

- the original paper or strongest available source was prioritized
- the selected reading mode matches the request
- difficult content was simplified in English before relying on Chinese
- Chinese adds depth rather than duplicating translation
- paper claims are separated from interpretation, inference, and project transfer
- technical terms are explained conceptually rather than as a glossary
- equations are connected to physical or algorithmic meaning
- experiment conclusions do not exceed the evidence
- project connections are limited, labeled, and technically grounded
- no missing paper detail was invented
- the answer remains focused on the user's actual reading target
