# AGENTS.md

## 1. Project Overview
Project name: Personal Knowledge Base
Project type: Personal document and knowledge management web application.

The application allows users to:
- Manage personal documents and files.
- Organize documents using folders and tags.
- Create notes and highlights linked to documents.
- Track reading progress.
- Search and filter stored documents.
- Use a local scripted AI Assistant demo.

## 2. Technology Stack
- HTML5
- CSS3
- Vanilla JavaScript
- localStorage
- IndexedDB

Do not use frameworks, libraries requiring a build step, or backend services unless explicitly approved.

The application must run directly in a browser without a build process.

## 3. Project Scope
Implement the following modules:
- Dashboard
- Document Library
- Folder Management
- Tag Management
- Document Details
- Notes and Highlights
- Reading Progress
- Search and Filtering
- AI Assistant Demo
- Application Settings
- Trash and Restore

The AI Assistant is a local scripted demonstration. It does not connect to an external AI API.

Real AI generation, automatic summarization, semantic search, and automatic knowledge graph generation are outside the current scope.

## 4. Core Development Rules
- Use clear, consistent naming conventions.
- Separate HTML structure, CSS styling, and JavaScript logic.
- Keep code modular and avoid unnecessary duplication.
- Use semantic HTML elements.
- Make the interface responsive for desktop, tablet, and mobile.
- Provide clear loading, empty, success, and error states where applicable.
- Validate user input before saving.
- Prevent invalid references between data entities.
- Avoid destructive operations without confirmation.
- Use accessible labels and keyboard-friendly interactions.
- Do not introduce features outside the approved project scope without authorization.

## 5. Data Management Rules
- Follow DATA_CONTRACT.md for all data structures and business rules.
- Do not independently redefine existing entity fields.
- Do not change relationships between entities without updating DATA_CONTRACT.md.
- Use localStorage for small settings and preferences.
- Use IndexedDB for structured application data and uploaded files.
- Do not store large binary files in localStorage.
- Handle storage failures and unavailable browser storage gracefully.
- Maintain data consistency when creating, editing, deleting, restoring, or linking entities.

## 6. Module Integration
- Each module must use the agreed data contract.
- Avoid duplicate implementations of shared services.
- Keep module-specific UI and logic separate where practical.
- Shared functions must have consistent input and output formats.
- Do not overwrite existing functionality when adding a module.
- Check dependencies before modifying shared files.

## 7. Change Management
Before implementing a task:
1. Understand the requested feature.
2. Inspect relevant existing files.
3. Identify affected modules and shared services.
4. Check DATA_CONTRACT.md for applicable rules.
5. Implement only the required changes.
6. Verify integration and regression risks.

If a requirement conflicts with an existing specification, identify the conflict before changing the specification.

## 8. Completion Criteria
A task is complete when:
- The requested functionality works.
- Data follows DATA_CONTRACT.md.
- Existing features remain functional.
- Input validation and error handling are implemented where necessary.
- Relevant test cases have been checked.
- Documentation is updated when contracts or workflows change.