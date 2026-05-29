# Coding Rules

## 1. KISS First, Always

**Keep It Simple, Stupid.**

- Prefer straightforward logic over clever tricks or patterns.
- If a junior developer couldn't explain the code in 2-3 sentences, it's too complex.
- Avoid unnecessary indirection (e.g., "manager of managers", nested factories, etc.).

**Agent behavior:**

- Default to the simplest solution that satisfies the requirements.
- Do not introduce abstractions or patterns unless they clearly simplify the codebase.

---

## 2. Be Ruthlessly DRY (But Not Dogmatic)

**Don't Repeat Yourself**, especially for logic and behavior.

- Extract shared logic into well-named functions or modules.
- Avoid copy-pasting the same behavior across files or components.
- However, don't create convoluted abstractions just to deduplicate a few similar lines.

**Agent behavior:**

- Look for repeated logic; encapsulate it in reusable functions.
- Prefer small, meaningful helper functions over generic "doEverythingUtil" helpers.
- It's okay to repeat a tiny bit of code if abstraction would obscure intent.

---

## 3. Avoid Over-Abstraction

Abstractions must **earn their keep**.

- Only abstract when there are **real, repeated patterns** and they are stable.
- Don't build meta-frameworks, super-generic base classes, or over-generic utilities.
- If an abstraction makes the mental model harder to understand, don't add it.

**Agent behavior:**

- Prefer concrete, domain-specific functions over hyper-generic helpers.
- Do not introduce complex inheritance trees or deep hierarchies.
- Avoid "just in case" abstraction for hypothetical future use.

---

## 4. Avoid Over-Engineering

Design for **today's real requirements**, not every hypothetical tomorrow.

- Apply **YAGNI**: You Aren't Gonna Need It.
- Don't add features, flags, extension points, or layers until there is a proven need.
- Avoid gold-plating: extra complexity without clear value.

**Agent behavior:**

- Implement only what is explicitly required or what is obviously necessary to make it robust.
- Do not speculate about future requirements or build for imaginary extensibility.

---

## 5. Fail Fast, Don't "Fallback Forever"

Too many fallbacks signal **low confidence** in the design.

- Each fallback should be **intentional**, **rare**, and **well-understood**.
- Prefer clear failure with good error messages over silently cascading through many fallbacks.
- "Try this, if not then this, then that, then that..." is a smell.

**Agent behavior:**

- Implement at most one or two clear, well-documented fallback paths where truly needed.
- When something is critical, fail fast with a clear error rather than guessing.

---

## 6. No Blanket Try/Catch as a Safety Blanket

Defensive coding is good; paranoia everywhere is not.

- Catch exceptions **only where they can be handled meaningfully**.
- Avoid blanket `catch (Exception)` / `try/except` sprinkled around every function.
- Unhandled exceptions should bubble up with context and be handled at a clear boundary (e.g., top-level handler, API boundary).

**Agent behavior:**

- Place try/catch/try-except blocks around specific risky operations, not whole functions.
- When catching, either:
    - recover in a well-defined way, or
    - log and rethrow / propagate with context.
- Do not hide failures or swallow exceptions silently.

---

## 7. Prefer Functional, Side-Effect-Minimal Code

Predictable code is easier to test and reason about.

- Functions should have clear inputs and outputs.
- Minimize hidden state and unexpected side effects.
- Side-effectful functions should have names that make side effects obvious (e.g., `saveUser`, `sendEmail`, `logEvent`).

**Agent behavior:**

- Decompose complex procedures into small, purpose-focused functions.
- When possible, keep helpers pure (no I/O, no global state changes).
- Make side effects explicit and isolated.

---

## 8. Optimize for Human Readability Over Cleverness

Code is read far more than it's written.

- Choose clarity over micro-optimizations unless profiling proves a real need.
- Use meaningful names; avoid abbreviations and cryptic naming.
- If the "clever" version needs a long comment to explain it, write the obvious version instead.

**Agent behavior:**

- Prefer explicit loops and conditionals over complex one-liners or deeply nested expressions.
- Add short, focused comments where intent is not obvious from the code itself.
- Respect existing naming and style conventions in the repo.

---

## 9. Keep Modules Small, Cohesive, and Well-Bounded

Good structure reduces complexity.

- Each module/class/component should do **one thing well**.
- Avoid "god objects" and massive utility modules that know about everything.
- Boundaries between modules should be clear and logical.

**Agent behavior:**

- Group related code together; don't scatter related behavior across many files without reason.
- When adding new functionality, consider whether it fits an existing module or deserves a small new one.
- Don't introduce cross-cutting dependencies that tangle unrelated parts of the codebase.

---

## 10. Build for Maintainability: Tests, Logs, and Contracts

Confidence comes from **design + verification**, not from piles of fallback logic.

- Add tests around critical and non-obvious logic.
- Validate inputs where appropriate and fail with clear messages.
- Log at meaningful boundaries with actionable, non-noisy messages.

**Agent behavior:**

- When adding complex logic, also add or update tests.
- Prefer simple, focused tests that check behavior over overly clever or brittle tests.
- Use logging thoughtfully: enough to help debug, not so much that it becomes noise.

---

## Summary for Agents

When generating or modifying code in this repository, ask:

1. **Is this the simplest solution that clearly solves the problem?**
2. **Am I repeating logic that should be shared?**
3. **Am I introducing abstractions or fallbacks just to feel "safe" rather than because they're needed?**
4. **Will a human reading this code later quickly understand what it does and why?**

If the answer to any of these is "no" or "not really", rewrite until it is.

Agents must prioritize:
**KISS -> DRY -> Readable -> Maintainable**
over cleverness, over-engineering, and defensive complexity.

# Research and Documentation Rules

## 1. Write for Digestibility, Not Completeness

**Brevity is a feature, not a limitation.**

- Summaries should be scannable—use headings, bullet points, and short paragraphs.
- Aim for information that can be absorbed in 2-3 minutes of reading.
- Cut filler words, excessive transitions, and formulaic phrases (e.g., "furthermore," "in addition," "it is important to note that").
- Use the **inverted pyramid**: lead with conclusions and key findings, then support with details.

**Agent behavior:**

- Produce concise summaries with clear structure: headers, short paragraphs (3-4 sentences max), and bullet lists for key points.
- Avoid overuse of cohesive devices and transition words—let organization and structure create flow.
- When documenting research, present findings in this order: conclusion first, supporting evidence second, methodology last.
- If a section exceeds 400 words, evaluate whether it can be split or condensed.

---

## 2. Make It Accessible to Junior Developers

**Write for understanding, not to impress.**

- Assume the reader is smart but unfamiliar with context-specific details.
- Define technical terms and jargon on first use with brief, inline explanations.
- Use concrete examples and analogies when explaining complex concepts.
- Avoid assuming deep domain knowledge—explain the "why" behind technical decisions.

**Agent behavior:**

- When introducing specialized terms, provide a one-sentence definition in parentheses or an inline clause.
- Use plain language by default; introduce technical vocabulary only when necessary and with context.
- Include practical examples that illustrate concepts rather than abstract descriptions.
- Structure explanations as: what it is -> why it matters -> how it works -> example.

---

## 3. Research Established Solutions First

**Favor proven approaches over novel implementations.**

- Before proposing a solution, investigate how the problem has been solved before.
- Document what has worked, what hasn't, and why.
- Identify common pitfalls, edge cases, and lessons learned from existing implementations.
- Establish whether the problem domain is well-understood or genuinely novel.

**Agent behavior:**

- Begin research by identifying 3-5 established solutions or approaches to the problem.
- Document each approach with: strengths, weaknesses, use cases, and known limitations.
- Explicitly state if a problem space is well-established vs. emerging vs. novel.
- Present findings as a comparison table when evaluating multiple solutions.

---

## 4. Default to "Buy" Over "Build"

**Building in-house should require clear justification.**

- Apply the **80/20 rule**: if an off-the-shelf solution meets 80% of requirements, strongly consider using it.
- Building custom solutions incurs hidden costs: maintenance, documentation, bug fixes, and knowledge transfer.
- Evaluate total cost of ownership, not just initial implementation cost.
- Custom builds are justified when: the problem is core to competitive advantage, existing solutions have unacceptable constraints, or long-term ownership cost is genuinely lower.

**Agent behavior:**

- When a problem is raised, first identify 2-3 existing tools, libraries, or services that address it.
- Present a build vs. buy analysis that includes: initial cost, maintenance burden, customization requirements, vendor lock-in risk, and time to value.
- Recommend "buy" by default unless there is a compelling reason to build.
- If recommending a custom build, explicitly state why existing solutions are insufficient.

---

## 5. Analyze Trade-Offs Explicitly

**Every solution has costs—make them visible.**

- No solution is purely good or bad; identify what is gained and what is sacrificed.
- Consider trade-offs across dimensions: cost, time, complexity, maintainability, performance, flexibility.
- Make trade-offs explicit so stakeholders can make informed decisions.
- Avoid presenting solutions as universally optimal.

**Agent behavior:**

- For each proposed solution, document trade-offs in a structured format:
    - **What you gain**: performance, simplicity, cost savings, speed, etc.
    - **What you sacrifice**: flexibility, maintenance burden, vendor dependency, etc.
    - **When this is the right choice**: specific conditions or contexts where this approach fits best.
- Use comparison tables to present multiple solutions side-by-side with their trade-offs.
- Avoid superlatives ("best," "optimal") unless you can objectively justify them.

---

## 6. Provide Constructive Pushback

**Challenge assumptions and question requirements when appropriate.**

- Don't default to affirmation—critically evaluate the problem and proposed solutions.
- Ask clarifying questions: Is this the right problem to solve? Are there hidden assumptions? Is the scope appropriate?
- Identify potential issues, risks, or alternative approaches that may not have been considered.
- Frame pushback constructively: explain the concern, provide reasoning, suggest alternatives.

**Agent behavior:**

- When a request seems over-scoped, under-specified, or potentially misguided, ask clarifying questions before proceeding.
- Raise concerns about: unclear requirements, scope creep, over-engineering, or misaligned solutions.
- Structure pushback as:
    1. **Observation**: What seems unclear or potentially problematic.
    2. **Reasoning**: Why this matters or what risks it introduces.
    3. **Suggestion**: Alternative approaches or clarifications needed.
- Distinguish between questions (seeking clarity) and concerns (identifying risks).

---

## 7. Separate AI Contribution Levels

**Be explicit about the extent of AI generation.**

- Clearly label AI-generated content according to contribution level:
    - **YOLO mode**: AI-generated without thorough review (use only for drafts/brainstorming).
    - **LLM Forward**: AI-generated first pass, carefully reviewed and edited by human.
    - **Mostly Me**: Human-authored with minor AI assistance (syntax, boilerplate, review).
- Verbose AI output increases the risk of conceptual errors being overlooked.
- Building intuition from source material is often more valuable than AI-generated summaries.

**Agent behavior:**

- Default to "LLM Forward" mode: generate content, but flag it as requiring human review and editing.
- When generating documentation, keep it concise to facilitate thorough human review.
- Do not generate verbose output that obscures errors or makes review burdensome.
- If a task requires deep understanding or intuition-building, recommend that the human engage with source material directly rather than relying solely on AI summaries.

---

## 8. Structure Research for Scannability

**Format findings so humans can process them quickly.**

- Use a hierarchical structure: H1 for the main topic, H2 for sections, H3 for subsections.
- Break content into digestible chunks: one idea per paragraph, one theme per section.
- Use visual hierarchy: bold for key terms, bullet lists for parallel items, tables for comparisons.
- Avoid walls of text—introduce whitespace and visual breaks.

**Agent behavior:**

- Use markdown formatting consistently: '#' for H1, '##' for H2, '###' for H3.
- Limit paragraphs to 3-5 sentences; break longer content into sub-sections.
- Use bullet points for lists of items, numbered lists for sequential steps.
- Use tables to compare multiple options across consistent criteria (e.g., features, cost, trade-offs).
- Bold key terms or findings to aid scanning.

---

## 9. Document Thoughtfully, Not Exhaustively

**Prioritize usefulness over completeness.**

- Focus on information that aids decision-making, understanding, or future maintenance.
- Avoid documenting the obvious—focus on the non-obvious: why decisions were made, what alternatives were considered, what constraints exist.
- Keep documentation close to the code or decision it describes.
- Update documentation when reality changes; outdated docs are worse than missing docs.

**Agent behavior:**

- When generating documentation, focus on:
    - **Why**: The reasoning behind decisions.
    - **Trade-offs**: What was gained and sacrificed.
    - **Gotchas**: Non-obvious pitfalls or edge cases.
    - **Context**: When this approach applies vs. when it doesn't.
- Do not document implementation details that are self-evident from the code.
- Avoid generating documentation that will quickly become outdated (e.g., specifics that change frequently).

---

## 10. Iterate Based on Feedback

**Documentation and research improve through use.**

- Treat initial drafts as living documents subject to refinement.
- Solicit feedback from the intended audience (junior devs, stakeholders, team members).
- Pay attention to where confusion or questions arise—these indicate gaps or unclear explanations.
- Simplify and clarify based on real-world usage patterns.

**Agent behavior:**

- When generating documentation, include a note indicating it should be reviewed and refined based on feedback.
- If asked to revise documentation, prioritize clarity and accessibility based on specific feedback.
- When confusion is reported, simplify language, add examples, or restructure content rather than adding more detail.
- Treat documentation as iterative: concise initial version -> gather feedback -> refine.

---

## Summary for Agents

When generating or modifying documentation and research in this repository, ask:

1. **Can a junior developer understand this in 3 minutes or less?**
2. **Have I researched established solutions before proposing something new?**
3. **Have I clearly documented trade-offs and made the "buy vs. build" case?**
4. **Am I providing constructive pushback where assumptions or scope need clarification?**
5. **Is this scannable and concise, or am I generating verbose content that will discourage thorough review?**

If the answer to any of these is "no" or "not really", revise until it is.

Agents must prioritize:
**Concise -> Accessible -> Thoughtful -> Actionable**
over exhaustive, verbose, or overly affirmative outputs.
