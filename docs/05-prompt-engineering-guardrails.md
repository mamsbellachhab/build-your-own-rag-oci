# Chapter 5 — Prompt Engineering & Guardrails

## Introduction

An agent that retrieves the right documents can still answer badly: inconsistent formatting, no source attribution, or confident guessing when the corpus has no answer. This chapter covers the two levers that shape agent behavior beyond retrieval itself — guardrails, which sit between the model and the user, and custom instructions, which shape how the RAG tool responds.

```mermaid
flowchart LR
    U[User input] --> GI[Input Guardrails<br/>Moderation / Prompt Injection / PII]
    GI --> AG[Agent + RAG Tool]
    AG --> GO[Output Guardrails<br/>Moderation / PII]
    GO --> R[Response to user]

    classDef guard fill:#f59e0b,stroke:#92400e,color:#fff
    classDef agent fill:#C74634,stroke:#8f2f22,color:#fff
    classDef io fill:#0B5FFF,stroke:#083d99,color:#fff

    class U,R io
    class GI,GO guard
    class AG agent
```

## Goal
Configure the agent's safety guardrails and tune the RAG tool's response behavior for grounded, well-formatted answers.

## Steps taken

### 5.1 Guardrails

During agent endpoint setup, all four guardrail categories (content moderation input/output, prompt injection protection, PII input/output) were reviewed.

![Content moderation options](images/ch05/15.png)

![Prompt injection and PII options](images/ch05/16.png)

**Decision: all guardrails set to Disable for this POC.**

This goes against the platform's own recommendation — Block is marked "recommended" for moderation and prompt injection. It was a deliberate choice for this internal, fictitious-data demo, not a default left unexamined.

```mermaid
flowchart TD
    subgraph Recommended production setup
        R1[Content moderation input: Block]
        R2[Content moderation output: Block]
        R3[Prompt injection: Block]
        R4[PII input: Block or Inform]
        R5[PII output: Block]
    end
    subgraph Used in this POC
        P1[Content moderation input: Disable]
        P2[Content moderation output: Disable]
        P3[Prompt injection: Disable]
        P4[PII input: Disable]
        P5[PII output: Disable]
    end

    classDef rec fill:#22c55e,stroke:#15803d,color:#fff
    classDef poc fill:#ef4444,stroke:#991b1b,color:#fff
    class R1,R2,R3,R4,R5 rec
    class P1,P2,P3,P4,P5 poc
```

![Review and create](images/ch05/17.png)

![Agent active](images/ch05/18.png)

### 5.2 Prompt / custom instructions

The RAG tool's custom instructions were edited after initial creation to enforce response formatting and strict grounding:

```
Response format:
1. Give a direct answer first.
2. If the answer involves multiple values (limits, dates, statuses), present them as a table.
3. Use bullet points for steps or lists.
4. End every response with a single line: "Source: [document name]"

Grounding rules:
- Only answer using information explicitly present in the knowledge base.
- Do not infer, extrapolate, or combine values across documents unless explicitly stated together.
- If the answer is not in the corpus, say so clearly instead of guessing.
```

![Edit tool, custom instructions](images/ch05/19.png)

## Design decisions
- **Guardrails disabled, documented as a conscious trade-off** rather than silently left at defaults.
- **Explicit grounding rules over implicit trust**: telling the model what to do when the answer isn't in the corpus is what makes the honesty check in Chapter 6 possible.

## Status
Complete
