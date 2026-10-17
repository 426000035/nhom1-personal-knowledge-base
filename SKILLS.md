# SKILLS.md

## 1. Purpose
This document defines reusable workflows for developing, testing, and integrating project modules.

It describes how work should be performed, not the application's data model or general coding rules.

For project-wide rules, refer to AGENTS.md.
For data structures and business rules, refer to DATA_CONTRACT.md.

## 2. Skill: Create a Module

### Goal
Implement one module without breaking existing functionality.

### Steps

1. Identify the module's purpose.
2. List the required screens and user interactions.
3. Identify the entities and services it needs.
4. Read the relevant sections of DATA_CONTRACT.md.
5. Inspect existing code for reusable components and services.
6. Define the module's inputs, outputs, and dependencies.
7. Implement the HTML structure.
8. Implement module-specific CSS.
9. Implement JavaScript behavior.
10. Connect the module to existing services.
11. Add validation and error handling.
12. Test the module's main workflows.
13. Document any new dependencies or changed contracts.

### Completion Checklist
- The module meets the requested requirements.
- Existing services are reused where appropriate.
- Data structures follow DATA_CONTRACT.md.
- Empty, success, and error states are handled.
- The module does not duplicate existing functionality.
- The module works at supported screen sizes.

## 3. Skill: Test a Module

### Goal
Verify that a module behaves correctly under normal and invalid conditions.

### Steps

1. Identify the module's main user workflows.
2. Test the normal successful workflow.
3. Test empty data.
4. Test missing or invalid input.
5. Test references to nonexistent entities.
6. Test duplicate data where uniqueness is required.
7. Test storage errors where practical.
8. Test boundary values.
9. Test deletion and restoration behavior where applicable.
10. Check that unrelated modules still work.

### Data Integrity Checks
- Every entity has a unique identifier.
- References point to existing entities.
- Deletion does not leave invalid references.
- Updates preserve fields that were not intentionally changed.
- Timestamps are updated when required.
- Stored data remains readable after refreshing the page.

### UI Checks
- Buttons perform their intended actions.
- Forms validate input.
- Confirmation dialogs appear before destructive operations.
- Empty states are clear.
- Error messages are understandable.
- Keyboard interaction and responsive layouts are usable.

### Completion Checklist
- Main workflows pass.
- Invalid input is handled safely.
- Data integrity rules pass.
- Existing functionality has not regressed.
- Remaining limitations are documented.

## 4. Skill: Integrate a Module

### Goal
Connect a completed module to the application without duplicating shared logic or breaking existing modules.

### Steps

1. Inspect the existing application structure.
2. Identify shared services, styles, navigation, and components.
3. Review the module's dependencies.
4. Compare its data usage with DATA_CONTRACT.md.
5. Reuse existing services wherever possible.
6. Resolve naming conflicts before merging code.
7. Integrate navigation and entry points.
8. Ensure shared CSS does not unintentionally affect other modules.
9. Verify storage operations and entity references.
10. Run the module's tests.
11. Run regression checks on related modules.
12. Update documentation if a contract or workflow changed.

### Integration Rules
- Do not create a second service for an existing responsibility without justification.
- Do not redefine shared entity fields inside an individual module.
- Do not overwrite shared files without inspecting their existing content.
- Avoid global variables unless they are part of the agreed application architecture.
- Keep module dependencies explicit and limited.
- Preserve existing routes, navigation, and user workflows.

### Completion Checklist
- The module is reachable through the application's navigation.
- Shared services work correctly.
- Data remains consistent across modules.
- Existing modules continue to function.
- No duplicate or conflicting implementations remain.

## 5. Skill: Change an Existing Feature

### Goal
Modify existing behavior while minimizing unintended side effects.

### Steps

1. Identify the requested change.
2. Locate the existing implementation.
3. Determine affected modules and services.
4. Check for dependencies on the current behavior.
5. Identify whether the data contract must change.
6. Implement the smallest sufficient change.
7. Test the modified behavior.
8. Test related workflows for regressions.
9. Update relevant documentation.

### Rules
- Do not rewrite unrelated modules.
- Do not remove existing functionality without approval.
- Do not silently change data formats.
- If a change conflicts with DATA_CONTRACT.md, resolve the conflict before implementation.

## 6. Skill: Debug an Issue

### Goal
Identify the cause of an issue before changing code.

### Steps

1. Reproduce the issue.
2. Record the expected behavior.
3. Record the actual behavior.
4. Inspect the relevant HTML, CSS, JavaScript, and service logic.
5. Check browser console errors.
6. Inspect stored data when the issue involves persistence.
7. Identify the root cause.
8. Apply a targeted fix.
9. Reproduce the original scenario.
10. Test nearby workflows for regressions.

### Rules
- Do not make unrelated changes during debugging.
- Do not hide errors without addressing their cause.
- Do not delete stored data as a default troubleshooting step.
- Document known limitations if a complete fix is not possible.

## 7. Skill: Handle a Data Contract Change

### Goal
Change the data model or business rules safely.

### Steps

1. Describe the reason for the change.
2. Identify affected entities and relationships.
3. Inspect every module that uses the affected fields.
4. Update DATA_CONTRACT.md first.
5. Define how existing stored data will be handled.
6. Update shared services.
7. Update affected modules.
8. Test creation, reading, updating, and deletion workflows.
9. Test compatibility with previously stored data.
10. Update related documentation.

### Rules
- Do not independently alter a field's meaning.
- Do not remove a field without checking its dependencies.
- Do not assume old local data matches the new schema.
- If data migration is necessary, implement and test it explicitly.

## 8. Skill: Prepare a Release

### Goal
Verify that the application is ready for demonstration or delivery.

### Steps

1. Review all required modules.
2. Check the main user workflows.
3. Test persistence after page refresh.
4. Test upload validation and file handling.
5. Test search and filters.
6. Test trash and restore.
7. Test responsive layouts.
8. Check browser console errors.
9. Verify that no external AI API is required for the demo.
10. Review known limitations.
11. Confirm that project documentation matches the implementation.

### Completion Checklist
- Required workflows function.
- Data persists as expected.
- No known critical errors remain.
- The application runs without a build process.
- Known limitations are documented.
- The demo can be run using the documented instructions.