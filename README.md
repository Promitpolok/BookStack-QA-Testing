# BookStack Demo — QA Testing Project

Manual functional testing, bug investigation, and automation test design for the BookStack Demo web application.

## Project Overview

**Application:** [BookStack Demo](https://demo.bookstackapp.com/)  
**Module Under Test:** Page Management  
**Testing Approach:** Manual Functional Testing and Automation Test Design  
**Test Environment:** Windows, Google Chrome  
**Automation Framework Proposed:** Playwright (JavaScript)

## Testing Objectives

- Verify page creation, editing, and deletion.
- Validate required fields and input handling.
- Test boundary values and special characters.
- Investigate concurrent page editing behavior.
- Identify regression scenarios suitable for automation.

## Test Execution Summary

| Metric | Result |
|---|---|
| Total Test Cases | 12 |
| Executed | 12 |
| Passed | 11 |
| Failed | 1 |
| Pass Rate | 91.67% |
| Reproduced Issues | 1 |

The failed test concerns concurrent page editing. The observed behavior did not meet the proposed conflict-safety expectation. Whether this constitutes a confirmed BookStack product defect depends on its documented concurrency requirements.

## Test Coverage

| Testing Category | Test Cases |
|---|---|
| Positive Testing | TC-01 to TC-04 |
| Negative Testing | TC-05 to TC-07 |
| Boundary Value Testing | TC-08 to TC-10 |
| Edge Case Testing | TC-11 to TC-12 |

## Bug Investigation

**BUG-001: Concurrent Page Editing Silently Overwrites Previous Changes**

When the same page was edited in two browser tabs, the second save replaced changes previously saved by the first tab without a visible conflict warning.

Earlier changes remained available through revision history.

See [Bug Report](Bug-Report.md) for reproduction steps and evidence.

## Automation Test Design

Three scenarios were selected for future automation using Playwright:

1. AT-01 — Create a page with valid data.
2. AT-02 — Validate an empty page title.
3. AT-03 — Concurrent page editing.

See [Automation Test Cases](Automation-Test-Cases.md).

Automation scripts have not been implemented or executed as part of this submission.

## Project Files

- [Functional Test Cases](Functional-Test-Cases.xlsx)
- [Bug Report](Bug-Report.md)
- [Automation Test Cases](Automation-Test-Cases.md)
- [Evidence Screenshots](evidence/)

## Conclusion

The testing demonstrated that core page management workflows behaved as expected across positive, negative, and boundary scenarios.

One concurrent-editing issue was reproduced and documented for further investigation.

## Disclaimer

This is an educational QA assignment conducted against the public BookStack Demo environment. It is not an official BookStack quality assurance report.