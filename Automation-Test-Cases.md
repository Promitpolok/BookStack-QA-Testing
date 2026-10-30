# Task 3: Test Automation Candidates

## Project Information

**Application:** BookStack Demo  
**Website:** https://demo.bookstackapp.com/  
**Module:** Page Management  
**Testing Type:** Functional Test Automation  
**Proposed Automation Tool:** Playwright  
**Browser:** Google Chrome / Chromium

---

## AT-01: Create a Page with Valid Data

**Related Functional Test:** TC-01  
**Test Type:** Positive Testing  
**Priority:** High

### Objective

Verify that a logged-in Admin can successfully create a new page with a valid title and content.

### Preconditions

- BookStack Demo is accessible.
- Admin account is available.
- Admin is logged in.
- Accounts Department book exists.

### Test Data

- Page Title: `QA Automation Test Page`
- Page Content: `This page was created for automated testing.`

### Automation Test Steps

1. Launch the browser using Playwright.
2. Navigate to the BookStack Demo website.
3. Log in using valid Admin credentials.
4. Open the Books section.
5. Select the Accounts Department book.
6. Click the New Page button.
7. Enter a unique page title.
8. Enter valid page content.
9. Click Save Page.
10. Verify that the saved page is displayed.
11. Verify that the page title and content match the input.
12. Delete the test page as cleanup.

### Expected Result

The page should be created successfully, and its title and content should be displayed correctly.

### Automation Assertions

- The saved page is visible.
- The page title matches the entered title.
- The page content matches the entered content.
- No unexpected validation error appears.

### Why Should This Test Be Automated?

Page creation is a core feature of BookStack. Automating this scenario saves time during regression testing and helps detect problems after application updates.

---

## AT-02: Validate Empty Page Title

**Related Functional Test:** TC-05  
**Test Type:** Negative Testing  
**Priority:** High

### Objective

Verify that BookStack prevents page creation when the title field is empty.

### Preconditions

- Admin is logged in.
- Accounts Department book is accessible.

### Test Data

- Page Title: Empty
- Page Content: `Testing empty title validation.`

### Automation Test Steps

1. Launch the browser.
2. Navigate to BookStack Demo.
3. Log in as Admin.
4. Open Accounts Department.
5. Click New Page.
6. Leave the page title field empty.
7. Enter valid page content.
8. Click Save Page.
9. Verify that a validation error appears.
10. Verify that the page remains in the editor.
11. Verify that no new page was published.

### Expected Result

BookStack should prevent saving the page and display the validation message:

`The name field is required.`

### Automation Assertions

- Validation message is visible.
- The editor remains open.
- No new page is published.

### Why Should This Test Be Automated?

Input validation is important for data quality. This test is simple, repeatable, and helps ensure that future updates do not accidentally allow pages with missing titles.

---

## AT-03: Concurrent Page Editing

**Related Functional Test:** TC-12  
**Test Type:** Edge Case / Regression Testing  
**Priority:** High

### Objective

Verify that BookStack handles conflicting edits to the same page without silently overwriting previously saved changes.

### Preconditions

- Admin account is available.
- A dedicated QA test page exists.
- Two browser tabs can access the same page.

### Test Data

- Initial Content: `Original content before editing.`
- Tab A Update: `Update from Tab A - First Save`
- Tab B Update: `Update from Tab B - Second Save`

### Automation Test Steps

1. Launch a browser using Playwright.
2. Log in as Admin.
3. Create a dedicated test page.
4. Open the page editor in Tab A.
5. Open the same page editor in Tab B.
6. Ensure both tabs have loaded the original page version.
7. Add the Tab A update in Tab A.
8. Save the changes from Tab A.
9. Return to Tab B without refreshing.
10. Add the Tab B update.
11. Attempt to save from Tab B.
12. Check whether BookStack displays a conflict warning.
13. Inspect the latest saved page content.
14. Check whether Tab A's update remains available.
15. Capture evidence of the result.
16. Delete the dedicated test page as cleanup.

### Expected Result

BookStack should detect conflicting changes and prevent silent overwriting, or provide an appropriate conflict-resolution mechanism.

### Automation Assertions

- A conflict warning or safe conflict-handling mechanism is triggered.
- Previously saved changes are not silently overwritten.
- Any rejected save is clearly communicated to the user.

### Why Should This Test Be Automated?

Concurrent editing can cause accidental data loss. Automating this scenario helps detect regression issues and verify that changes to the editor do not introduce silent overwriting.

### Related Bug

**BUG-001:** Concurrent Page Editing Silently Overwrites Previous Changes.

The manual test demonstrated that saving a stale second tab replaced the first tab's update in the latest page version without a warning. The earlier version remained recoverable through revision history.

---

## Automation Summary

| Automation ID | Scenario                      | Test Type              | Priority |
| ------------- | ----------------------------- | ---------------------- | -------- |
| AT-01         | Create a Page with Valid Data | Positive               | High     |
| AT-02         | Validate Empty Page Title     | Negative               | High     |
| AT-03         | Concurrent Page Editing       | Edge Case / Regression | High     |

## Conclusion

These three scenarios are suitable for automation because they cover core functionality, input validation, and conflicting page edits.

Playwright is the proposed automation framework because it supports browser interaction, multiple tabs, and automated assertions.

**Automation Status:** Test cases designed; scripts not implemented or executed.

**Note:** The expected conflict-protection behavior in AT-03 is a proposed quality requirement. It should be checked against BookStack's official concurrency behavior before classifying the observed result as a confirmed product defect.
