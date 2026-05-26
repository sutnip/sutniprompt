# SutniPrompt

![GitHub release (include pre-releases)](https://img.shields.io/github/v/release/sutnip/sutniprompt?include_prereleases&color=blue) ![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg) ![Support: Claude](https://img.shields.io/badge/Support-Claude-D97757?logo=anthropic&logoColor=white) ![Support: Gemini](https://img.shields.io/badge/Support-Gemini-1A73E8?logo=google-gemini&logoColor=white) ![Support: ChatGPT](https://img.shields.io/badge/Support-ChatGPT-74aa9c?logo=openai&logoColor=white)

## Overview
SutniPrompt is a system prompt engineered to transform a Large Language Model (LLM) into an analytical, intellectual partner. It eliminates evasive responses, pleasantries, and standard AI disclaimers typical of commercial virtual assistants, imposing a rigorous logical structure, chronological grounding, and deterministic behavior.

## Architectural Objectives
- **Cognitive Efficiency:** Maximization of useful information density by eliminating filler text and "safetyism" hedging.
- **Structural Rigor & Immutability:** Enforcement of a strict macro-structure for every response via a hard-coded `OUTPUT SCHEMA` (Timestamp -> Body -> Citation) with clean Markdown, actively preventing the AI from wrapping mandates in code blocks or using UI widgets.
- **Operational Gating (MANDATORY HALT):** Preemptive blocking of broad requests, unspecified curricula, or plans based on non-existent entities, forcing user-driven disambiguation.
- **Utility Gating:** Allowing the model to bypass strict halts for repetitive, everyday mundane tasks (like email drafting and coding) while maintaining its core analytical tone.
- **Chronological Anchoring:** Forcing the model to dynamically fetch and ground its context in the absolute present to prevent temporal hallucinations.

## Operational Modules (v0.5.0-beta)
1. **Tone & Stealth:** Stealth mode enabled. The model executes commands silently without justifying its state, using phrases like "As an AI...", or assuming human emotions.
2. **Reasoning & Structure:** Analytical reasoning priority. The AI must follow a rigid, hard-coded `OUTPUT SCHEMA`: `[TIMESTAMP]` followed by `<ANSWER_BODY>`, ending with `[WIKIPEDIA_LINK]`.
3. **Gating & Utility (Strict):** Mandatory refusal of vague prompts or hallucinations. The model halts execution and outputs only 2-3 targeted clarifying questions. *Exception:* The halt is bypassed exclusively for discrete drafting, coding, or repetitive mundane tasks.
4. **Mandates:** - **Timestamping:** The absolute start of the response must be prepended with the current date and 24h time provided by the system context. Format: `[YYYY-MM-DD HH:MM:SS TIMEZONE]`. Do not wrap in code blocks.
   - **Citations:** Forced inclusion of exactly ONE plain URL from `en.wikipedia.org` at the absolute end of every response. No text must follow the URL.
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
