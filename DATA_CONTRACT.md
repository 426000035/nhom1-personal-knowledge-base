# DATA_CONTRACT.md

## 1. Purpose
This document defines the application's data models, relationships, business rules, storage strategy, and service contracts.

All modules must follow these definitions.

## 2. Data Models

### 2.1 Document
Represents a stored document or external resource.

Fields:
- id: string
- title: string
- type: string
- sourceType: string
- sourceUrl: string | null
- fileName: string | null
- mimeType: string | null
- fileSize: number | null
- storageKey: string | null
- folderId: string | null
- tagIds: string[]
- description: string
- status: string
- priority: string
- createdAt: string
- updatedAt: string
- lastOpenedAt: string | null
- deletedAt: string | null

Allowed type values:
- pdf
- epub
- txt
- markdown
- mobi
- azw
- url

Allowed sourceType values:
- file
- url

Allowed status values:
- unread
- in_progress
- read

Allowed priority values:
- low
- normal
- high

Rules:
- A document must have a unique id.
- A document must have a non-empty title.
- A file document must reference its stored file through storageKey.
- A URL document must have a valid sourceUrl.
- folderId may be null when the document is not assigned to a folder.
- tagIds contains references to existing tags.
- deletedAt is null when the document is active.
- updatedAt changes whenever the document is modified.

### 2.2 Folder
Represents a folder used to organize documents.

Fields:
- id: string
- name: string
- parentId: string | null
- createdAt: string
- updatedAt: string

Rules:
- Folder names must not be empty.
- parentId may be null for a root folder.
- Nested folders are supported without a predefined depth limit.
- A folder cannot be its own parent.
- Folder relationships must not contain cycles.
- A folder can only be deleted when it has no documents and no child folders.

### 2.3 Tag
Represents a classification label.

Fields:
- id: string
- name: string
- color: string
- createdAt: string
- updatedAt: string

Rules:
- Tag names must not be empty.
- Tag names must be unique after trimming whitespace and applying case-insensitive comparison.
- A tag can be associated with multiple documents.
- A tag can only be deleted when it is not used by any document.

### 2.4 Note
Represents a user's note.

Fields:
- id: string
- title: string
- content: string
- documentIds: string[]
- createdAt: string
- updatedAt: string

Rules:
- A note may exist independently of documents.
- A note may be linked to multiple documents.
- documentIds must reference existing documents.
- Deleting a document removes its reference from documentIds.
- Deleting a document must not automatically delete an associated note.

### 2.5 Highlight
Represents selected text associated with a document and a note.

Fields:
- id: string
- documentId: string
- noteId: string
- selectedText: string
- startOffset: number | null
- endOffset: number | null
- createdAt: string

Rules:
- Each highlight belongs to exactly one document and one note.
- documentId and noteId must reference existing entities.
- selectedText must not be empty.
- If offsets are available, startOffset must be less than or equal to endOffset.
- Deleting the referenced note removes its highlights.
- Deleting the referenced document removes its highlights.

### 2.6 ChatMessage
Represents a message in the local AI Assistant demo.

Fields:
- id: string
- role: string
- content: string
- createdAt: string

Allowed role values:
- user
- assistant

Rules:
- content must not be empty.
- The assistant uses predefined local command-handling logic.
- Supported demo operations include searching, filtering, and retrieving recent documents.
- The assistant must not create, edit, or delete application data.
- Chat history must not be treated as an authoritative data source.

### 2.7 ReadingProgress
Represents a user's reading position.

Fields:
- id: string
- documentId: string
- position: number
- progressPercent: number
- updatedAt: string

Rules:
- documentId must reference an existing document.
- position must be zero or greater.
- progressPercent must be between 0 and 100.
- Reading progress is optional.
- Deleting a document removes its reading progress.

### 2.8 AppSettings
Represents application preferences.

Fields:
- id: string
- theme: string
- defaultView: string
- itemsPerPage: number

Allowed theme values:
- light
- dark
- system

Allowed defaultView values:
- grid
- list

Rules:
- itemsPerPage must be a positive integer.
- Default theme is system.
- Default view is grid.
- Default itemsPerPage is 12.

## 3. Relationships

- Folder has a one-to-many hierarchical relationship with child folders.
- Folder can contain multiple documents.
- Document belongs to zero or one folder.
- Document and Tag have a many-to-many relationship.
- Note and Document have a many-to-many relationship.
- Highlight belongs to one Document and one Note.
- ReadingProgress belongs to one Document.
- ChatMessage is independent of document data.
- AppSettings stores application preferences.

## 4. File Handling Rules

Supported extensions:
- .pdf
- .epub
- .txt
- .md
- .markdown
- .mobi
- .azw

Maximum upload size: 10 MB per file.

Rules:
- Validate file extension and size before accepting an upload.
- Use IndexedDB to store uploaded file data.
- Use storageKey to associate a document with its stored file.
- Handle unsupported file formats with a clear error message.
- File metadata extraction must not be assumed to work for every format.
- URL metadata retrieval may fail because of browser CORS restrictions.
- PDF and EPUB annotation behavior must be validated against the chosen reading implementation.

## 5. Storage Strategy

### localStorage
Use for small, non-binary data such as:
- Theme preferences
- Default view
- Pagination preferences
- Other small application settings

### IndexedDB
Use for:
- Documents
- Folders
- Tags
- Notes
- Highlights
- Reading progress
- Uploaded file data
- Other structured application data that requires reliable browser storage

Rules:
- Do not store uploaded binary files in localStorage.
- Handle unavailable or full browser storage.
- Do not assume local browser data automatically synchronizes across devices.
- Do not claim that local data is backed up unless a backup mechanism exists.

## 6. Deletion and Trash Rules

- Soft-deleted documents have a non-null deletedAt value.
- The trash retention period is 30 days.
- Documents in trash must not appear in normal document searches.
- A document may be restored within the retention period.
- If its original folder no longer exists, ask the user to choose another folder or restore it without a folder.
- Permanent deletion removes the document and its stored file data.
- Associated notes are preserved, but references to deleted documents are removed.
- Highlights and reading progress referencing a permanently deleted document are removed.

## 7. Search and Filtering

Supported document search fields:
- title
- description
- fileName
- sourceUrl

Supported filters:
- folder
- tags
- document type
- reading status
- priority
- creation date
- trash status

Rules:
- Search and filters must be combinable.
- Deleted documents are excluded from normal search.
- Trash search includes only deleted documents.
- Full-text search inside PDF, EPUB, and other file contents is not included unless separately approved.

## 8. Service Contracts

All data services must use consistent return structures.

Success:
{
  "success": true,
  "data": {},
  "error": null
}

Failure:
{
  "success": false,
  "data": null,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message"
  }
}

Recommended service responsibilities:

DocumentService:
- createDocument(data)
- getDocumentById(id)
- listDocuments(filters)
- updateDocument(id, data)
- softDeleteDocument(id)
- restoreDocument(id)
- permanentlyDeleteDocument(id)

FolderService:
- createFolder(data)
- listFolders()
- updateFolder(id, data)
- deleteFolder(id)

TagService:
- createTag(data)
- listTags()
- updateTag(id, data)
- deleteTag(id)

NoteService:
- createNote(data)
- getNoteById(id)
- listNotes(filters)
- updateNote(id, data)
- deleteNote(id)

HighlightService:
- createHighlight(data)
- listHighlights(filters)
- deleteHighlight(id)

ReadingProgressService:
- getProgress(documentId)
- saveProgress(documentId, data)
- deleteProgress(documentId)

SettingsService:
- getSettings()
- updateSettings(data)

The exact implementation may vary, but service behavior and data rules must remain consistent.

## 9. Error Handling

Use consistent error codes where applicable:
- VALIDATION_ERROR
- NOT_FOUND
- DUPLICATE_ENTRY
- INVALID_REFERENCE
- FILE_TOO_LARGE
- UNSUPPORTED_FILE_TYPE
- STORAGE_ERROR
- OPERATION_NOT_ALLOWED
- UNKNOWN_ERROR

Error messages must explain the problem and, where possible, how to resolve it.

## 10. Explicitly Excluded Features

Unless separately approved, do not implement:
- User accounts or authentication
- Cloud synchronization
- External AI API integration
- Automatic AI summaries
- Semantic search
- Automatic knowledge graph generation
- Bulk document operations
- Duplicate document detection
- Version history
- Full-text indexing of uploaded files