# PathReview Development Journal

**Name:** Christian A Gomez Diaz
**GitHub Username:** Christian101GTZ

---

# Week 7 — Issue Selection

**Issue link:** https://github.com/ascherj/pathreview/issues/148

**Issue title:** Skill extractor fails to detect JavaScript and TypeScript

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

### Problem Summary

The skill extractor currently does not recognize JavaScript and TypeScript when they appear in a resume or profile document. As a result, these programming languages are missing from the extracted skills even though they are valid technologies. This affects the ingestion pipeline because the application may produce incomplete skill data. A successful fix will update the skill extraction logic and related tests so JavaScript and TypeScript are detected correctly. This ensures resumes containing these technologies are analyzed more accurately.

### Issue Selection Notes

I selected this issue because it is focused on a single part of the ingestion pipeline and has a clear expected outcome. The problem is well defined: JavaScript and TypeScript should be recognized as valid skills during extraction. It is an appropriate first contribution because the scope is manageable while still requiring me to understand and modify production code and its related tests. Based on the issue checklist, I believe I can complete it without needing to understand the entire codebase.

**Branch name:** `fix/148-skill-extractor-javascript-typescript`

**Setup confirmation:** [x] App runs locally at `localhost:5173`

**Cohort ledger:** [x] Issue added to cohort ledger 

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/Christian101GTZ/pathreview/commit/81ff1ad

**Reproduction summary:**

I reproduced Issue #148 by running the existing TypeScript unit test:

`pytest tests/unit/test_skill_extractor.py::TestSkillExtractor::test_text_with_typescript_files -v`

The test failed because the extractor did not return TypeScript for text containing TypeScript-specific syntax. I also compared extraction with and without a `.ts` filename. Without a filename, the extractor incorrectly returned Python. With `example.ts`, it returned both Python and TypeScript.

**PLAN.md link:** https://github.com/Christian101GTZ/pathreview/blob/fix/148-skill-extractor-javascript-typescript/PLAN.md

**Walkthrough video (recommended):** Not recorded.

**Blockers or open questions:**

The Python type-annotation pattern matches `str` inside the TypeScript type `string`, creating a false Python result. I still need to determine the safest detection patterns for distinguishing JavaScript, TypeScript, and Python without introducing false positives.