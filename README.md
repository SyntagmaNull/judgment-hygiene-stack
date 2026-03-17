# Judgment Hygiene Stack

A tri-skill routing and output-discipline framework for LLMs.

This repository contains a structured pipeline for handling messy user input without collapsing into:
- premise smuggling
- fake grounding
- verification sprawl
- synthetic completion over abstention
- safety signal dilution
- structurally pretty but epistemically weak answers

## What this is

This stack separates three different jobs that are often incorrectly mixed together in a single model response:

1. **structure_judgment**  
   Diagnose what kind of problem the prompt actually is.

2. **verification_hygiene**  
   If external facts are needed, retrieve and filter evidence without treating the internet as an oracle.

3. **judgment_hygiene**  
   Produce the final answer with clean dependency structure, honest abstention, and explicit tradeoff discipline.

These skills are connected through a strict handoff spec defined in `PIPELINE_CONTRACT.md`.

## Why this exists

LLMs often fail in recurring structural ways:

- presenting inference as observation
- escalating action from a user’s emotionally loaded interpretation
- searching biased queries that confirm the user’s premise
- treating SEO consensus as evidence
- smoothing uncertainty into polished but false completion
- swallowing safety-bearing language because another layer feels easier to answer

This stack is designed to reduce those failure modes without flattening all model-specific judgment into one rigid style.

## Repository contents

```
judgment-hygiene-stack/
├─ README.md
├─ LICENSE
├─ PIPELINE_CONTRACT.md
└─ skills/
   ├─ structure_judgment/SKILL.md
   ├─ verification_hygiene/SKILL.md
   └─ judgment_hygiene/SKILL.md
```

- `skills/structure_judgment/SKILL.md`  
  Front-end routing skill. Determines the real problem shape before answering.

- `skills/verification_hygiene/SKILL.md`  
  External evidence discipline. Controls search/query formation, source weighting, and abstention on dead ends.

- `skills/judgment_hygiene/SKILL.md`  
  Final answer discipline. Controls observation/inference separation, grounding, tradeoffs, abstention, and anti-performance checks.

- `PIPELINE_CONTRACT.md`  
  Defines stage order, payload interfaces, abstention propagation, and bounded model-specific variation.

## Design principles

- **guardrails, not flattening**
- **search for facts, not opinions**
- **abstention is better than synthetic completion**
- **routing is not answering**
- **verification is not judgment**
- **final polish is not permission to erase uncertainty**
- **safety signals must be triaged, not auto-believed and not ignored**

## Current status

**Controlled trial / release candidate**

This repository is not presented as a production-perfect safety or truth system.
It is a structured skill stack intended for:
- agent trial runs
- benchmark testing
- pipeline experimentation
- failure-mode reduction in judgment-bearing outputs

## Non-goals

This stack does **not** guarantee:
- factual truth
- moral correctness
- legal or medical sufficiency
- immunity to bias
- elimination of all hallucinations
- universal agreement across models in boundary cases

It improves one layer only:
**structural hygiene in routing, verification, and judgment-bearing output generation.**

## Intended use

This stack is meant to be installed as a multi-skill system in agents that support skill-based execution or staged prompting.

Recommended order:


structure_judgment
→ verification_hygiene (only if triggered)
→ judgment_hygiene

See PIPELINE_CONTRACT.md for the exact interface.



## **Known limitations**

- boundary cases still require model judgment
    
- multimodal provenance remains harder than text-only verification
    
- “clean structure” does not equal “correct conclusion”
    
- safety triage still contains hard edge cases, especially around rhetoric vs distress
    
- different models may resolve boundary prompts differently inside the guardrails
    
