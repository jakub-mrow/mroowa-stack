---
name: mroowa-teach
description: Explain a change, concept, or subsystem so the user understands what it is, how it works, and why it is designed that way. Use for teach me this, help me understand X, or a requested guided explanation.
license: MIT
---

# Teach

Explain at the person's pace. The goal is understanding, not changing the code.

Adapted from pstack's teach skill for a smaller token budget. This version removes required sibling skill invocations, parallel investigations, and generated images.

## Ground the explanation

- Infer the user's purpose and existing knowledge from the conversation. Focus on the few things they need to understand to review, debug, change, or use the subject. Skip concepts they already understand.
- Reuse code exploration and evidence already gathered in this session. Read the relevant code, diff, or documentation directly when evidence is missing. Work in the current agent by default; delegate only when the user requests it or the scope justifies it within the session's delegation rules.
- Trace the mechanism before explaining it. Investigate design history only when the rationale matters to the question, starting with the relevant commits or documentation rather than a broad search.
- Separate documented rationale from inference. Preserve uncertainty from the source and say when a reason is unknown. Cite concrete files or sources when they help the user follow the explanation.

## Teach in layers

1. Start with the smallest complete explanation, usually one or two sentences. Define the thing in plain language and connect it to the user's actual code or situation.
2. When the user asks for more, walk through one concrete example: the trigger, what happens next, how the data changes, and the result. Explain the problem the mechanism solves instead of listing functions and constants.
3. Add deeper reasons, tradeoffs, and edge cases when they matter. Keep terminology consistent. Prefer the actual mechanism to a loose analogy.
4. Use a short code example, Mermaid diagram, or ASCII sketch when it clarifies more than prose. For complex flows, add one component at a time as the explanation progresses. Diagrams and images are optional; do not generate images automatically.
5. Stop at a natural conversational boundary and let the user choose the next depth. Do not quiz them, ask them to repeat the explanation, or announce artificial pauses. For a requested one-shot explanation, provide the requested depth in one response.

## Response

Deliver the explanation itself, not a report about your research. Use plain spoken language, short sentences, and concrete examples. Avoid stock framing phrases, unnecessary headers, and a long introductory preview. Offer a specific next detail only when useful.
