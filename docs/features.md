# Features

[← Back to Pineria](../README.md)

What Pineria does, and where each thing stops. Limits are stated next to the feature they belong to
rather than buried at the end — finding them out the hard way is worse.

---

## Browsing

A file browser that reads the disk directly, so you can browse folders you have never indexed.

- List, details and grid views, switchable per session — grid tiles show the thumbnail Windows
  already keeps for photos, videos and PDFs, cached after the first look; anything Windows has no
  thumbnail for shows its file-type icon
- Breadcrumbs that collapse sensibly on deep paths
- Back, forward and up, with `Alt+←`, `Alt+→` and `Alt+↑`
- Quick access to Desktop, Documents, Downloads, Pictures, Music, Videos and every drive letter
  that responds
- Pin any file or folder to the sidebar
- Recently opened list, clearable at any time
- Right-click for Explorer integration: reveal in Explorer, open with the default program, open a
  terminal here, copy the full path

> **Worth knowing.** A folder listing stops at 20,000 entries and tells you it was truncated.
> Hidden-file filtering uses the name convention — a leading `.` or `$` — rather than the Windows
> hidden attribute.

## Search

Fast search over every indexed file name and path.

| Filter | What it does |
| --- | --- |
| Free text | Matches from the start of each word, in names and paths |
| Type | Images, video, audio, documents, code, archives, applications |
| Extension | Offered from the extensions actually present in your archive |
| Tag | Anything carrying the tags you pick |
| Size | Above, below or between |
| Date | Modified within a range |
| Folder | Restrict to one folder and everything beneath it |

Sort by name, size, type, or modified and created date. The match count shown is exact.

> **Worth knowing.**
> - Matching starts at a word boundary: `proj` finds `project`, `roje` finds nothing.
> - It searches names and paths only, never the text inside documents.
> - Results are capped at 500 rows by default and 5,000 at most. The *count* is always exact.
> - Search sees what the last scan indexed. Files added since then are invisible until you rescan.

## Tags

Coloured labels that work across folders and drives.

- As many tags per file as you like; one tag can span your whole archive
- Applied to a whole selection at once
- Colour-coded, with a live count in the sidebar
- Right-click a tag to rename it, recolour it, or delete it — deleting removes the label only and
  never touches a file
- Drag a selection onto a tag in the sidebar to apply it
- Tagging is undoable

> **Worth knowing.** Tags follow files when you move or rename them **inside** Pineria. Move a file
> in Explorer and the connection is lost at the next scan.

## Collections

Two kinds, for two different habits.

**Manual collections** hold files you add by hand — a reading list, a project's scattered assets,
anything that does not deserve its own folder. Drag files onto one in the sidebar to add them.

**Smart collections** save a search and re-run it every time you open them, so they are always
current. Five are created on first run:

| Collection | What it holds |
| --- | --- |
| Large Files | Anything 100 MB and over, biggest first |
| Changed in 30 Days | A rolling window of recent work |
| PDF Archive | Every PDF, newest first |
| Photos | Every image |
| Video Library | Every video, biggest first |

> **Worth knowing.** Smart collections cannot have files added by hand — edit the rule instead.
> Collections reference files; deleting a collection never deletes anything.

## Duplicates

![Duplicate groups with reclaimable space](../assets/duplicates.png)

Finds byte-for-byte identical files, cheaply:

1. Group by exact size — pure index work, nothing read from disk
2. Fingerprint the first 64 KB of the survivors
3. Full SHA-256 checksum only for files that still match

Most of an archive never gets opened, which is why a scan finishes in seconds. Results show each
group, the space it wastes, and a **keep** choice per group.

> **Worth knowing.** Nothing is deleted for you. *Bin the others* sends the copies you did not keep
> to the Recycle Bin. Checksums are remembered and only recalculated when a file's size or date
> changes, so a second scan over an unchanged archive is nearly instant.

## Archive health

A read-only audit. It reports; it changes nothing.

- Indexed files that are no longer on disk
- Very large files (4 GB and above) worth a second look
- Zero-byte files — usually failed downloads
- Empty folders
- A summary of space lost to duplicates

> **Worth knowing.** The missing-file check samples the 4,000 most recently indexed entries rather
> than walking your whole archive, so it stays fast. The duplicate line only appears once you have
> run a duplicate scan at least once.

## Preview

See a file without opening another program.

| Type | Shown as |
| --- | --- |
| Images | The picture, with dimensions |
| Video and audio | An inline player |
| PDF | A page viewer |
| Text, Markdown, code, CSV | The contents, with the language noted |
| ZIP | A listing of what is inside |
| Anything else | Its details, with a plain explanation |

Every file also shows type, size, created, modified and accessed dates, its full path, and its tags.

> **Worth knowing.** Text previews show the first 512 KB. Files above the size limit in Settings are
> not previewed, except video and audio, which stream. ZIP contents are listed, never extracted.
> Other archive formats are not read in this version.

## File operations and undo

Create folders, rename, move, copy, and send to the Recycle Bin — with the safety rules that define
this application:

- **Deletion is Recycle Bin only.** There is no permanent-delete anywhere in Pineria.
- **Nothing is overwritten silently.** A name collision becomes `name (2).ext`.
- **Protected locations are refused.** Drive roots, Windows, Program Files and ProgramData are
  rejected for every write, whatever asked for it.
- **Everything is undoable.** `Ctrl+Z` and `Ctrl+Shift+Z`, plus a full history you can browse and
  undo individually (`Ctrl+K` → *Show operation history*).

> **Worth knowing.** Recycle Bin deletions are the one exception to undo: Windows owns the restore,
> so you bring those back from Explorer. Everything else reverses from inside Pineria.

## The Archive Organizer

A dedicated workspace for restructuring an archive by hand: four resizable columns, your current
folders facing the structure you want, and a short drag across the middle to move files. Queue
hundreds of moves, review them, apply them at once — and undo the whole batch with one `Ctrl+Z`.

[The full guide →](archive-organizer.md)

## Dashboard

![The archive overview](../assets/dashboard.png)

Totals for files, folders and space; the split by file type; your largest files; what changed most
recently; how much space duplicates are wasting; and when the last scan ran.

## Settings

Seven sections: General, Appearance, Indexing, Files, Privacy, Backup and About.

Themes are **dark**, **light** and **system**, which follows Windows and switches live.

![Pineria in light mode](../assets/light.png)

Under Indexing you manage your archive folders — add, rescan, or remove one. Removing a folder from
the index never touches the folder itself, and your tags are kept.

## Backup and export

- **Export metadata** writes your tags, collections, pins and settings to a single JSON file. File
  contents are never included.
- **Import** merges an export back in and never deletes anything.
- **Back up the database** takes a full copy of the index, safe to run while the app is open.

## Keyboard shortcuts

| | |
| --- | --- |
| `Ctrl+K` | Command palette — everything, searchable |
| `Ctrl+F` | Search |
| `Ctrl+B` | Show / hide the sidebar |
| `Ctrl+P` | Show / hide the preview pane |
| `Ctrl+A` | Select all |
| `Ctrl+C` `Ctrl+X` `Ctrl+V` | Copy, cut, paste |
| `Ctrl+Z` `Ctrl+Shift+Z` | Undo, redo |
| `Ctrl+Shift+N` | New folder |
| `F2` | Rename |
| `F5` | Refresh |
| `Delete` | Send to the Recycle Bin |
| `Space` | Toggle preview |
| `T` | Tag the selection |
| `Enter` | Open |
| `Alt+←` `Alt+→` `Alt+↑` | Back, forward, up |
| `Escape` | Unwind one layer |
| `M` `C` `Q` | In the Organiser: move, copy, queue |

Everything on a shortcut is also in the command palette and the right-click menu.

## Not in this version

- macOS and Linux builds
- Automatic updates
- Search inside document contents
- A live filesystem watcher — the index updates when you scan
- Code signing, which is why Windows warns on first run
- Archive preview beyond ZIP listings
