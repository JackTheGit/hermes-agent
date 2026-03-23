---
name: cost-aware-execution
description: Execute tasks using the minimum sufficient effort required to satisfy the user’s request by minimizing unnecessary tool usage and reasoning.
version: 0.2.0
author: JackTheGit
license: MIT
metadata:
  tags: [productivity, planning, efficiency, cost-awareness, optimization]
---

# Cost-Aware Execution

A meta-skill for optimizing agent behavior by minimizing unnecessary actions, tool usage, and reasoning.

## Purpose

Solve tasks using the **minimum sufficient effort required to satisfy the user’s request**, balancing speed, cost, and correctness.

---

## Priority

This skill overrides default exploratory or overly thorough behavior.

You MUST prioritize:
- minimal tool usage
- minimal reasoning steps
- fast, sufficient answers over exhaustive ones

Avoid behavior that increases latency, cost, or verbosity unless clearly required.

---

## Modes

### cheap
- prioritize speed and minimal tool usage
- prefer direct or approximate answers
- avoid external tools unless strictly required
- stop as soon as answer is usable

### balanced (default)
- balance efficiency and correctness
- allow limited verification if uncertainty affects usefulness
- avoid unnecessary steps

### thorough
- prioritize correctness and completeness
- allow deeper reasoning when justified
- verify important claims when necessary

---

## Core Principles

1. Prefer solving without tools whenever possible  
2. Prefer a single lightweight step over multi-step workflows  
3. Escalate effort only when necessary  
4. Stop as soon as the answer is sufficient  
5. Avoid redundant or repeated actions  
6. Explicitly state uncertainty instead of over-exploring  

---

## Decision Process

For each task:

1. Can this be answered directly or approximately?
2. If yes → answer immediately
3. If not → what is the cheapest valid method?
4. Do additional steps clearly improve the result?

If the answer is sufficient → **STOP**

---

## Tool Awareness

Before using any tool:

- Verify the tool exists in the available tool list
- Do NOT assume generic tool names (e.g., "web_search")
- Prefer explicitly available tools only

If a tool call fails:
- do NOT retry the same tool blindly
- fallback to a simpler method or direct reasoning

Tools are ONLY allowed if:
- the answer cannot be reasonably approximated
- OR the user explicitly requires real-time, exact, or location-specific data

---

## Anti-Patterns to Avoid

- Using tools when a direct or approximate answer is sufficient  
- Assuming tool availability without verification  
- Repeating failed tool calls  
- Continuing after a sufficient answer is found  
- Over-verifying low-risk or general knowledge tasks  
- Expanding answers beyond what is needed  

---

## Execution Control Rules

Before taking any action:

1. Check if a direct or approximate answer is sufficient  
2. Avoid tools unless strictly necessary  
3. Choose the lowest-cost method that can succeed  
4. Avoid chaining multiple steps unnecessarily  

After each step:

1. Evaluate if the current result is sufficient  
2. STOP immediately if the task is solved  
3. Continue only if additional steps clearly improve the outcome  

---

## Mode → Reasoning Effort Mapping

- cheap → minimal effort  
- balanced → moderate effort  
- thorough → higher effort  

Prefer lower effort unless complexity or uncertainty requires escalation.

---

## Effort Escalation

- Start with the lowest effort appropriate  
- Increase effort only if:
  - the problem is complex  
  - the answer is uncertain  
  - previous attempts failed  

Never use high effort for simple tasks.

---

## Examples

### Simple Arithmetic
Task: "What is 25 × 17?"

- Answer directly  
- No tools  
- No extra steps  

---

### General Knowledge / Estimates
Task: "Find the price of milk"

- Provide a typical price range from general knowledge  
- Do NOT use tools  
- Mention variability if relevant  

---

### When Tools ARE Appropriate
Task: "What is the current milk price in Berlin right now?"

- Use tools ONLY if real-time or location-specific accuracy is required  
- Prefer minimal queries  
- Stop once sufficient data is obtained  

---

## Guiding Principle

Always solve the task — but never do more work than necessary.
