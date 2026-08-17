# Changelog

[← Back to Pineria](README.md)

What changed in each release, written for the people using it.

---

## 0.1.1 — 17 August 2026

Five fixes from real use. Install over 0.1.0; your index, tags and collections are kept.

### Folders of photos load properly now

A grid tile is about 112 pixels wide, but Pineria was pointing it at the original file — so opening
a folder of forty photos meant decoding forty full-size images. On a real photo library that showed
as tiles arriving slowly, or never arriving.

Tiles now use the thumbnail Windows already keeps, cached on disk. Measured on 24 photos: **23,639 KB
of originals becomes 811 KB of thumbnails**, decoded at 256×160 rather than 1920×1200. The cache keys
on each file's size and date, so an edited photo refreshes its own tile.

### Right-click works in the Archive Organizer

Files, folders in either index, and the empty space around them now have a menu: open, move or copy
to the other side, add to the queue, rename, new folder, pin as a quick destination, tag, show in
Explorer, copy path, and move to the Recycle Bin. Rename and delete each ask first, and both undo
with `Ctrl+Z`.

### The two organizer panes no longer open on the same folder

The right side prefers a second archive folder when you have one. When both sides do point at the
same place it says so, and offers to pick another folder or create a new one — which then opens on
the right, ready to receive files.

### Duplicates can be acted on in bulk

Select copies across groups with a running total of the space you would free; **Select every extra
copy** respects whichever copy you marked as the keeper; expanding a group shows every property of
each copy — modified, created and opened dates, size, extension, tags and full path; and a floating
bar sends the selection to the Recycle Bin at once. The copy marked *keeping* can never be selected,
so the last one cannot be deleted by accident.

### Archive health can tidy what it finds

Empty folders, zero-byte files and files reported missing can be ticked and cleared in one go rather
than only listed. The duplicate summary line stays unselectable, being a headline rather than a file.

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
