# Changelog

[← Back to Pineria](README.md)

What changed in each release, written for the people using it.

---

## 0.1.0 — 17 August 2026

The first public release.

### Find things

- **Archive index.** Nominate folders and Pineria indexes them in the background. Scanning is
  read-only, incremental, and can be stopped and resumed — a cancelled scan still leaves a usable
  index.
- **Search** across every indexed name and path, in milliseconds, with combinable filters for type,
  extension, tag, size, date and folder.
- **Tags.** Coloured labels that work across folders and drives, applied to a whole selection at
  once, and carried along when you move or rename files inside Pineria.
- **Collections.** Manual ones hold files you add by hand; smart ones save a search and re-run it
  every time. Five smart collections are set up on first run.

### Understand things

- **Overview** of the whole archive: totals, the split by file type, largest files, recent changes,
  and space lost to duplicates.
- **Duplicate detection** that compares sizes, then a partial fingerprint, then a full SHA-256 —
  so most of the archive is never read from disk.
- **Archive health**, a read-only audit reporting missing files, very large files, zero-byte files,
  empty folders and duplicates.
- **Preview** for images, video, audio, PDF, text, Markdown, code, CSV and the contents of ZIP
  archives, without opening another program.

### Reorganise things

- **The Archive Organizer** — a four-column workspace with your current folders facing the structure
  you want, so a move is a short drag across the middle. Multi-select, drag and drop, quick
  destinations, and per-side search and filters.
- **A queue** that stages work without touching the disk until you apply it.
- **Conflict handling** that stops before moving anything and offers Keep both, Skip or Replace —
  where even Replace routes the displaced file through the Recycle Bin.
- **Plan mode**, for sketching a folder structure that does not exist until you create it, with six
  starter templates.
- **Rules and suggestions** that propose moves for you to approve, and never act on their own.
- **Crash recovery.** A batch writes down what it intends to do before the first file moves, so an
  interrupted move can be finished, rolled back or accepted on the next launch.

### Keep things safe

- Deletion goes to the Recycle Bin. There is no permanent-delete anywhere in the application.
- Moves and copies never overwrite silently — a collision becomes `name (2).ext`.
- Drive roots and the Windows, Program Files and ProgramData folders are refused for every write.
- Undo and redo across moves, copies, renames, folder creation and tagging, with a browsable
  history. A batch of any size is a single undo step.
- No network client, no telemetry, no account. Nothing leaves the machine.

### Get around

- Command palette on `Ctrl+K`, reaching everything the app can do.
- A full keyboard map, with every shortcut also available from a menu.
- Dark, light and system themes; list, details and grid views.
- Metadata export and import, and on-demand database backups.

### Known limits in this release

- Windows 10/11 only — no macOS or Linux build.
- Not code-signed, so Windows SmartScreen warns on first run.
- No automatic updates; updating means installing the next release over the top.
- Search matches from the start of a word and covers names and paths, not the text inside documents.
- The index changes when a scan runs — there is no live filesystem watcher yet.
- Recycle Bin deletions are restored from Windows Explorer, not from inside Pineria.
- ZIP is the only archive format whose contents can be listed.
