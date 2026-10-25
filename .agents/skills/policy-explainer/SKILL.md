---
name: policy-explainer
description: Explains insurance policy terms, coverage, exclusions, and limits in plain words for customers, using only the policy text provided. Use whenever the user shares an insurance policy or clause and asks "is X covered", "what does this mean", "explain my policy", "what is excluded", or asks for a customer-friendly summary of policy wording, even if they do not say "explain".
---

# Policy Explainer

## Before starting
You need the policy text. If the user asks about coverage but has not shared
the policy, ask for it. Never answer coverage questions from general knowledge.

## Workflow
1. Read the policy. Find the parts that matter to the question:
   coverage, exclusions, limits, deductible, waiting period, conditions.
2. Answer using ONLY what the policy says. Quote the clause number or heading.
3. Explain each term in plain words. Use `references/plain-words.md` for common terms.
4. Write the answer in the format below.

## Answer format
**Short answer:** one or two sentences. Use "Covered", "Not covered", "Covered with conditions", or "Not clear in this policy".

**What the policy says**
- The relevant clause (number or heading) and what it means in plain words

**What is excluded or limited**
- Exclusions, caps, deductible, waiting period that affect this question

**An example:** one small everyday example using made-up numbers

**What to confirm with the insurer:** anything unclear, or anything that depends on facts of the case

End every answer with: "This is an explanation of the policy wording, not a claim decision. The final decision rests with the insurer."

## Rules
- Use only the policy text. Never fill gaps from what "most policies" say.
- If the policy does not address it, say "Not clear in this policy". Do not guess.
- Never promise a claim will be paid, and never say it will be rejected.
- Keep numbers exactly as written (amounts, days, percentages). Do not round.
- Use words a school student could follow. Explain any term you must keep.
- If the user shares personal data, do not repeat it back unless needed.
- Write in the language the user wrote in.

## Gotchas
- Exclusions can sit far from the coverage section, in "General Exclusions" or the schedule. Read the whole document before answering.
- "Covered" often has conditions (waiting period, pre-authorization, sub-limits). Do not say plain "Covered" if conditions exist.
- Deductible is what the customer pays first. Sub-limit is a smaller cap inside the main limit. Do not mix them up.
