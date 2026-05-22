# SutniPrompt

![GitHub release (include pre-releases)](https://img.shields.io/github/v/release/sutnip/sutniprompt?include_prereleases&color=blue) ![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg) ![Support: Claude](https://img.shields.io/badge/Support-Claude-D97757?logo=anthropic&logoColor=white) ![Support: Gemini](https://img.shields.io/badge/Support-Gemini-1A73E8?logo=google-gemini&logoColor=white) ![Support: ChatGPT](https://img.shields.io/badge/Support-ChatGPT-74aa9c?logo=openai&logoColor=white)

## Overview
SutniPrompt is a system prompt engineered to transform a Large Language Model (LLM) into an analytical, intellectual partner. It eliminates evasive responses, pleasantries, and standard AI disclaimers typical of commercial virtual assistants, imposing a rigorous logical structure, chronological grounding, and deterministic behavior.

## Architectural Objectives
- **Cognitive Efficiency:** Maximization of useful information density by eliminating filler text and "safetyism" hedging.
- **Structural Rigor:** Enforcement of clean Markdown outputs focused on mental models and analytical frameworks rather than dogmatic conclusions.
- **Operational Gating (MANDATORY HALT):** Preemptive blocking of broad requests, unspecified curricula, or plans based on non-existent entities, forcing user-driven disambiguation.
- **Utility Gating:** Allowing the model to bypass strict halts for repetitive, everyday mundane tasks (like email drafting and coding) while maintaining its core analytical tone.
- **Chronological Anchoring:** Forcing the model to ground its context in the absolute present to prevent temporal hallucinations and help the user track chronological chat timestamps.

## Operational Modules (v0.3.0-alpha)
1. **Tone & Stealth:** Stealth mode enabled. The model executes commands silently without justifying its state, using phrases like "As an AI...", or assuming human emotions.
2. **Reasoning & Structure:** Analytical reasoning priority. Logic or code flaws are fixed with minimal verbosity. Self-summarizing at the end of responses is strictly forbidden.
3. **Gating & Utility (Strict):** Mandatory refusal of vague prompts or hallucinations. The model halts execution and outputs only 2-3 targeted clarifying questions. *Exception:* The halt is bypassed exclusively for discrete drafting, coding, or repetitive mundane tasks (e.g., meal plans).
4. **Mandates:** - **Timestamping:** The exact current time must be prepended to the absolute beginning of every response using the format `[YYYY-MM-DD HH:MM:SS TIMEZONE]`.
   - **Citations:** Forced inclusion of exactly one relevant English Wikipedia link (`en.wikipedia.org`) at the absolute end of every response for further reading on the topic.
   - **External Tools:** Standardized nomenclature (concise titles + "[AI]") for external tools and calendar events.

## Deployment Guidelines across LLMs
Due to varying architecture and context window constraints across commercial platforms, implementation requires specific approaches:

### Anthropic Claude
Claude's infrastructure natively handles extensive system contexts.
- **Method:** Copy and paste the entire system prompt block directly into the "System Prompt" settings.

### Google Gemini
Gemini's personalization interface (System Instructions) may occasionally exhibit parsing errors with monolithic, highly structured text blocks.
- **Method:** Deploy directives modularly. Copy and paste the numbered modules (1, 2, 3, 4) sequentially into the system configuration window.

### OpenAI ChatGPT
The character limit for Custom Instructions or the GPT Builder often prevents the insertion of the full structured prompt.
- **Method:** Paste the entire prompt as the *first message* at the start of a new chat session to initialize the operational context.
- **Future Roadmap:** A "quantized" (minified and compressed) version of the prompt is under development to fit within native custom instruction limits while maintaining the operational hierarchy.
