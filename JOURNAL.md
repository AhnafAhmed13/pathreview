## Week 7 — Issue selection

**Issue link:** [Issue #147](https://github.com/ascherj/pathreview/issues/147)

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**

The `resume parser` is expected to parse section headers in resume. However, because of indentations (leading whitespaces), the section headers are not being detected by the parser. Involves `_detect_sections()` in `ingestion/parsers/resume_parser.py`

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger