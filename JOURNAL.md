## Week 7 — Issue selection

**Issue link:** [Issue #147](https://github.com/ascherj/pathreview/issues/147)

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**

The `resume parser` is expected to parse section headers in resume. However, because of indentations (leading whitespaces), the section headers are not being detected by the parser. Involves `_detect_sections()` in `ingestion/parsers/resume_parser.py`

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger


## Week 8 — Reproduction & solution planning

**Reproduction commit link:** [link to commit documenting the reproduced issue](https://github.com/AhnafAhmed13/pathreview/commit/2f7d407fc48626eb757a8b3f590c5c8013df32e0)

**Reproduction summary:**

Created a `test.py` file and used the following code:
```py
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(res.metadata['detected_sections'])
# observed: []  (expected: Education, Skills)
```

**PLAN.md link:** [link to PLAN.md in your fork](https://github.com/AhnafAhmed13/pathreview/blob/fix/147-resume-section-whitespace/PLAN.md)

**Walkthrough video (recommended):** [link to your Loom video, ≤2 min — shared for early feedback]

**Blockers or open questions:**
[Anything you're still uncertain about going into Week 9, or leave blank]


## Week 9 — Solution building & PR submission

### Check-in 1 (mid-week)

**Current progress:**
I have implemented the following code in `resume_parser.py`
```py
patterns = [
                rf"^[ \t]*{re.escape(section)}\s*$",
                rf"^[ \t]*{re.escape(section)}\s*[:|-]",
                rf"\n[ \t]*{re.escape(section)}\s*$",
                rf"\n[ \t]*{re.escape(section)}\s*[:|-]",
            ]
```
This extends the regex patterns in `resume_parser.py` to include leading whitespaces/indentations.

I have added `test_parse_section_with_whitespace` test in `test_resume_parser.py` to validate fix.


**Next steps:**
Create pull request

**Blockers:**
[Anything slowing you down? Or leave blank.]