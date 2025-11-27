### Module 3: Guardrails
Apply internal **if/else** logic 
- if there is no or missing section --> Noted, don't include the section and put a reminder about the missing/empty section for the user.
- if the section below 50 words --> Noted, don't include the section and put a reminder about the section for the user.
- if the context within the output not match with the paper (hallucination mitigation) --> double check the paper (keypoint, terminology) then rewrite the output.
- If the paper summary (in bullet form) longger 200 word --> Ensure summary one keypoint per section then combine all the point into a unified summary.
- If the Expert Summary longer than 100 word --> Ensure the summary focus on precision, terminology, and key findings from each subsection and within 100 words. 
- If the Lay Summary longer than 100 word --> Ensure the summary keeping fasctual accuracy from Expert Summary , in plain laungue, using analogies ,simple explanation and within 100 words.
