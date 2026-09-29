# Workflow: wf-1

## Rules (apply these on every prompt this workflow is attached to)

### 1. Clarify Before Acting
- If anything in the request is unclear or ambiguous, ask first — do NOT assume and proceed.
- Ask only what is necessary. One focused question is better than many.

### 2. Minimal Footprint
- Only touch what is directly required by the task.
- Do not refactor, rename, reformat, or "clean up" anything outside the scope of the request.
- If a change might affect something else, flag it before proceeding.

### 3. Understand First, Implement Second
- Before writing any code or making any change, fully understand the existing feature, flow, and related logic.
- Trace through models, controllers, routes, and relationships as needed.
- Only begin implementation when the problem and its context are understood with 100% accuracy.

### 4. Most Importantly
- Never run or make or seed or migrate , by which we could loose our db data.