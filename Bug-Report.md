# BUG-001 — Concurrent page editing silently replaces an earlier update

**Application:** BookStack Demo  
**URL:** https://demo.bookstackapp.com/  
**Module:** Page Management  
**Date tested:** 2026-10-30  
**Browser:** Google Chrome on Windows  
**Severity:** Medium (provisional)  
**Status:** Reproduced in demo; classification against documented requirements pending  
**Related test:** TC-12

## Description
Editing the same page in two tabs, then saving stale content from the second tab, replaced the first tab's changes in the latest page revision without a conflict warning. The earlier update remains recoverable in revision history.

## Steps to reproduce
1. Sign in as Admin to BookStack Demo.
2. Create a dedicated QA page containing `Original content before editing.`
3. Open the same page editor in Tab A and Tab B, both initially showing the original content.
4. In Tab A, append `Update from Tab A - First Save` and save.
5. Without refreshing Tab B, append `Update from Tab B - Second Save` and save.
6. Inspect the latest page content and the Revisions view.

## Expected result
The application should detect the stale edit and warn the user or offer a safe conflict-resolution workflow before overwriting a newer saved version. This is a proposed quality expectation, not yet verified as an official BookStack requirement.

## Actual result
Revision #2 contained the Tab A update. Revision #3 contained the Tab B update but not the Tab A update. The tester reported that no conflict warning appeared on the second save. Revision #2 remained in history.

## Impact
A user can unintentionally remove another session's edits from the current page. Revision history mitigates permanent loss, but restoration requires manual action.

## Evidence
- [Tab A saved — Revision #2](evidence/TC-12-Tab-A.png)
- [Tab B saved — Revision #3](evidence/TC-12-Tab-B.png)
- [Revision history — versions #1–#3](evidence/BUG-001-Revision-History.png)

## Suggested improvement
Detect stale versions on save, warn users about conflicting updates, and allow comparison or conflict resolution.

## Limitations
The issue was reproduced in one Chrome session with two tabs on a public demo. Verify against official concurrency specifications before claiming it is a confirmed upstream product defect.
