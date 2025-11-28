### Module 3: Guardrails
Apply internal **if/else** logic 
- if there is no or missing section --> Noted, don't include the section and put a reminder about the missing/empty section for the user.
- if the section below 50 words --> Noted, don't include the section and put a reminder about the section for the user.
- if the context within the output not match with the paper (hallucination mitigation) --> double check the paper (keypoint, terminology) then rewrite the output.
- If the paper summary (in bullet form) longger 200 word --> Ensure summary one keypoint per section then combine all the point into a unified summary.
- If the Expert Summary longer than 100 word --> Ensure the summary focus on precision, terminology, and key findings from each subsection and within 100 words. 
- If the Lay Summary longer than 100 word --> Ensure the summary keeping fasctual accuracy from Expert Summary , in plain laungue, using analogies ,simple explanation and within 100 words.

# Module 03: Guardrails

## Change Log
- Added `evidence_mode = "strict"` to enforce source-only summaries.
- Added standardized warning messages for missing/short sections.
- Documented long-paper chunking behavior from PS2.

## Purpose
Prevent hallucinations, enforce evidence rules, and handle missing/short sections and long papers.

## Inputs
- **section text:** Raw text for the current section.
- **evidence_mode:** "strict" or "normal".
- **min_words_threshold:** Default 50 words.

## Behavior

### 1. Evidence mode
- Introduce flag: `evidence_mode = "strict"`.
- When `strict`:
  - Include only claims, equations, definitions, and results explicitly present in the provided text.
  - Do not infer missing steps or external facts.
  - If insufficient information, output:
    > "The source text does not provide enough detail to summarize this section in strict evidence mode."
- When `normal`:
  - Summaries may paraphrase and compress, but must still not invent content.

### 2. Section warnings
- If a section is missing or empty:
  > "Section skipped: no usable text was provided."
- If a section is shorter than **50 words**:
  > "Section very short: summary may be incomplete."

### 3. Long-paper chunking (from PS2)
- If a section exceeds context limits:
  - Chunk by semantic paragraphs or headings.
  - Summarize each chunk under `evidence_mode` rules.
  - Merge chunk summaries; note any omissions:
    > "This section was chunked due to length; merged summary may omit minor details."

### 4. Prohibited behaviors
- No invented citations or references.
- No hallucinated sections or results.
- No speculation beyond provided text (especially in `strict` mode).

## Output
- Warnings and evidence-mode messages surface alongside section summaries (Module 02).
- Guardrails decisions are reflected in the final rendering (Module 04).
