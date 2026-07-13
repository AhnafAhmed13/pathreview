## Week 7 — Issue selection

**Issue link:** [https://github.com/jamjamgobambam/pathreview/issues/2](https://github.com/jamjamgobambam/pathreview/issues/2)

**Issue title:** Skill extractor ignores Python type annotations when identifying Python usage


**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**

The `SkillExtractor` language detector in [skill_extractor.py](https://github.com/jamjamgobambam/pathreview/blob/main/ingestion/parsers/skill_extractor.py) is supposed to recognize when a file is Python, but its type hint signal is too narrow to catch modern, annotation-heavy code.

Right now it only matches variable annotations for six builtin types `int|str|float|bool|list|dict` and has no detection at all for return type annotations `-> str`, so files whose primary Python signal is type hints, stubs, Protocol definitions, or code using types like `bytes, tuple, Optional[X]`, or custom classes can score zero evidence and be misclassified as not Python. This weakens skill extraction accuracy for any ingested source that leans on type hints rather than imports and def keywords.

A successful fix would broaden the annotation detection to cover `->` return hints and a general identifier pattern for annotations, so that a file that is predominantly type-annotated is reliably credited as Python without introducing false positives on non-Python text.


**Branch name:** fix/2-skill-extractor-python-type-hints

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [?] Issue added to cohort ledger