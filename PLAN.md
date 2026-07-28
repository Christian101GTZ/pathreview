## Solution plan

**Issue:** Issue #148 – Skill extractor fails to detect JavaScript and TypeScript

### Understand

The skill extractor does not correctly detect JavaScript and TypeScript from resume text. The TypeScript test fails because the current logic mainly relies on the `.ts` file extension instead of recognizing TypeScript syntax. I also found that `id: string` is mistakenly detected as Python because the Python regex matches `str` inside `string`.

### Map

Files involved:

* `ingestion/parsers/skill_extractor.py`
* `tests/unit/test_skill_extractor.py`

### Plan

1. Update the language detection logic for JavaScript and TypeScript.
2. Prevent TypeScript syntax from being incorrectly detected as Python.
3. Update or add unit tests to verify the fix.
4. Run the tests to make sure everything passes.

### Inputs & outputs

**Input:**

* Resume text containing JavaScript, TypeScript, or Python code.
* Optional filenames such as `.js` or `.ts`.

**Output:**

* JavaScript resumes should detect JavaScript.
* TypeScript resumes should detect TypeScript.
* Python should continue to be detected correctly.
* TypeScript should no longer be incorrectly detected as Python.

### Risks & unknowns

* JavaScript and TypeScript have similar syntax, so they must be distinguished correctly.
* Changing the Python detection could accidentally affect valid Python detection.
* Additional test cases may be needed if unexpected behavior appears.

### Edge cases

* TypeScript without a `.ts` filename.
* JavaScript without a `.js` filename.
* Mixed-language resumes.
* Valid Python type annotations should still work correctly.
