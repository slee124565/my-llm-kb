# OpenAI Prompt Engineering - GPT-3.5 Era

## Source Metadata

- Source URLs:
  - https://help.openai.com/en/articles/6654000-comprehensive-step-by-step-guide-to-prompt-engineering-with-chatgpt
  - https://cookbook.openai.com/articles/techniques_to_improve_reliability
  - https://developers.openai.com/api/docs/guides/prompt-engineering
- Author: OpenAI
- Published:
  - Help Center article: updated after original GPT-3.5-era guidance; exact original publication date not captured here
  - Cookbook reliability article: 2022-09-12
  - Current Prompt engineering docs: living documentation
- Captured: 2026-05-03
- Capture method: OpenAI docs MCP plus official OpenAI-domain web search
- Scope note: This is not a `gpt-3.5-codex` model-specific guide. It captures the older GPT-3/GPT-3.5 and pre-agent Codex-era prompting style that OpenAI documented around clear instructions, delimiters, output examples, decomposition, and reasoning scaffolds.

## Source Notes

OpenAI's classic API prompt engineering guidance centers on making the model's desired behavior explicit in the prompt:

- use the latest capable model because newer models tend to need less prompt work
- place instructions before context and separate context with delimiters such as triple quotes or section markers
- be specific about outcome, context, length, format, style, and audience
- show the desired output format with examples when parseability matters
- tune `model` and `temperature` for quality, cost, latency, and determinism

The older reliability guidance adds a second theme: when a model fails on complex reasoning, improve reliability by giving it more structure:

- ask it to reason before answering when the task needs multi-step inference
- split complex tasks into smaller subtasks
- sample multiple candidate answers for some discrete-answer tasks
- constrain outputs to reduce hallucination
- fine-tune or build external systems when prompt-only reliability stops scaling

The current OpenAI Prompt engineering docs preserve the same foundations while reframing them for the Responses API:

- developer instructions have higher priority than user input
- Markdown and XML tags help mark prompt boundaries
- reusable prompts, prompt versions, and evals make prompts production artifacts
- few-shot examples are useful when behavior or format cannot be specified reliably in prose
- RAG and context-window planning matter when answers depend on external knowledge

## Durable Takeaway

The GPT-3.5-era prompt design mindset was prompt-as-instruction: write clearer instructions, add examples, use delimiters, break tasks down, and prompt the model to reason when it lacks reliability. This style treats the model as capable but brittle, so the prompt carries much of the structure that later moves into tool contracts, evals, runtime state, and agent harnesses.
