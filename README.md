# AI Toolbox 🧰

A collection of drop-in AI building blocks to drop into any repository.

## Tools

### 1. Agent Instructions (`AGENT.md`)
**The "Brain" for your AI Agents.**  
A drop-in set of rules and design philosophies that force AI agents (like Gemini, Cursor, or GitHub Copilot) to produce high-quality, readable, and maintainable code.

- **Why it matters:** Prevents AI "hallucinations" of complex patterns and enforces KISS (Keep It Simple, Stupid) and DRY (Don't Repeat Yourself) principles.
- **How to use:** Drop `AGENT.md` into your project root and instruct your AI assistant to follow it.

### 2. GitLab MR Reviewer (`gitlab_reviewer.py`)
**Surgical, automated code reviews.**  
A lightweight script that analyzes GitLab Merge Request diffs using the latest LLMs and posts actionable findings as line-scoped discussions.

- **Latest Model:** Defaults to `openai/gpt-5.5-thinking`.
- **Surgical:** Focuses only on changed lines to minimize noise.
- **Multi-provider:** Supports any model via [litellm](https://github.com/BerriAI/litellm).

---

## Quick Start

### Local Reviewer Setup
1. **Install:**
   ```bash
   uv pip install aiohttp litellm tiktoken
   ```

2. **Run:**
   ```bash
   export GITLAB_TOKEN="your_token"
   export LLM_API_KEY="your_key"
   uv run gitlab_reviewer.py
   ```

### GitLab CI Integration (Drop-in)
Add this to your `.gitlab-ci.yml` for instant AI reviews:

```yaml
ai-mr-review:
  stage: review
  image: python:3.11-slim
  variables:
    LLM_MODEL_ID: "openai/gpt-5.5-thinking"
    AI_REVIEW_REQUIRED: "false"
  before_script:
    - pip install --quiet aiohttp litellm tiktoken
  script:
    - python gitlab_reviewer.py
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
  allow_failure: true
```

## Design Philosophy

This toolbox is built on the principles defined in `AGENT.md`:
- **KISS First:** Simple logic over clever tricks.
- **Ruthlessly DRY:** No logic repetition.
- **Readable:** Optimized for humans, not just compilers.
- **Fail Fast:** No silent fallbacks.

## License
MIT
