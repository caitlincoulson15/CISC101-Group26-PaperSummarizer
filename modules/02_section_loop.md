### Module 2: Section Loop (within the paper)
- For each section 
    - Focus on main idea and keypoint.
    - Summarize each section in a keypoint.
- Combine all the keypoints into a summary within 200 words.

# Module 02: Section Loop

## Change Log
- Added `summary_level` variable to control summary length.
- Implemented conditional logic for "short" and "detailed" summaries.
- Clarified formatting and guardrail application order.

## Purpose
Iterate through each section of the paper, generate summaries, and enforce constraints.

## Inputs
- **sections:** List of (name, text) pairs extracted from the paper.
- **summary_level:** "short" or "detailed".
- **evidence_mode:** Passed through from Module 03 (e.g., "strict" or "normal").

## Behavior
For each section:
1. **Normalize text:** Trim whitespace, remove formatting artifacts, detect missing/empty text.
2. **Apply guardrails (Module 03):**
   - If missing/empty: output standardized warning and skip.
   - If < 50 words: output standardized warning, then proceed with cautious summary.
   - Respect `evidence_mode` rules.
3. **Summarization logic (conditional by `summary_level`):**
   - If `summary_level = "short"`:
     - Produce a compact 1–2 sentence summary capturing the main contribution, result, or idea in the section.
   - If `summary_level = "detailed"`:
     - Produce a short paragraph summary (3–5 sentences) focusing on purpose, method, and key findings.
     - Add a bullet list of **3–5 key points** (facts, definitions, results, equations referenced by name or number).
4. **Evidence constraints:**
   - Only include claims explicitly present in the source section (see Module 03).
   - If insufficient evidence in strict mode, state:  
     > "The source text does not provide enough detail to summarize this section in strict evidence mode."
5. **Output format (per section):**
   - **Section:** <name>
   - **Summary:** <text>
   - If `summary_level = "detailed"`:  
     - **Key points:**  
       - <point 1>  
       - <point 2>  
       - <point 3>  
       - (optional) <point 4–5>
6. **Combine section outputs** in order to form the Section-by-Section Table in rendering.

## Notes
- Do not invent sections or citations.
- Keep language precise and neutral.
- Defer chunking decisions to Module 03 when sections exceed context limits.
