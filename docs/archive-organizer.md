# Archive Organizer

[← Back to Pineria](../README.md)

**Left is what you have. Right is where it should go.** Files cross the middle.

That is the whole idea. Everything below is detail.

The Organiser exists because reorganising a large archive in Windows Explorer is miserable: you lose
your place, you cannot see both ends at once, a mistake is hard to undo, and nothing tells you what
is actually in a folder before you open it. This is a workspace built for that one job.

Open it from the left rail (**Organise**) or with `Ctrl+K` → *Open Archive Organizer*.

---

## The layout

Four columns:

```
┌───────────┬──────────────────┬──────────────────┬───────────┐
│  folder   │ folder contents  │ folder contents  │  folder   │
│  index    │                  │                  │  index    │
│           │  CURRENT         │  NEW             │           │
│ (where    │  what is in the  │  what is in the  │ (where    │
│  you are) │  folder you      │  folder you      │  things   │
│           │  picked          │  picked          │  go)      │
└───────────┴──────────────────┴──────────────────┴───────────┘
```

The **indexes** on the outside show structure only — folders, not files — so you can navigate a deep
archive without losing sight of what you are carrying. The **contents** face each other in the
middle, which is what makes a move a short drag rather than a journey.

Everything is adjustable and the app remembers nothing you did not ask it to:

- Drag any divider to resize. Double-click a divider to reset it.
- **Hide indexes** folds the outer columns away and gives the contents the full width.
- **Hide preview** (`Ctrl+P`) reclaims the preview pane's width.
- The library sidebar folds away by itself when you open the Organiser, and comes back when you
  leave. `Ctrl+B` overrides that in either direction — once you decide, Pineria stops deciding for
  you.

Each side has its own root selector at the top of its index, so the two sides can be in completely
different places — a photo drive on the left, a documents drive on the right.

## Reading a folder before you open it

Each index entry shows a **file count for everything beneath it**, not just its immediate contents.
That is how you spot the folder holding 40,000 files before you click into it.

Under the contents, the **overview** strip summarises the current folder: subfolders, total files,
total size, when it last changed, and a coloured bar showing the split by file type.

> **These counts come from the index, so they are as fresh as your last scan.** Files added outside
> Pineria will not appear until you rescan. This is the one number in the Organiser that can be
> stale, and it is worth remembering when something looks wrong.

## Selecting files

| | |
| --- | --- |
| Click | Select one |
| `Ctrl` + click | Add or remove one |
| `Shift` + click | Select a range |
| `Ctrl+A` | Everything currently listed — including everything hidden by scrolling |
| `Escape` | Clear the selection |

The bar along the bottom always shows what is selected, how much it weighs, and where it is headed.
Selecting a file also previews it, if the preview pane is open.

`Ctrl+A` respects the filter and the search box. Filter to **Images**, press `Ctrl+A`, and you have
selected every image in the folder and nothing else.

## Four ways to move something

1. **Drag onto a folder in either index.** The clearest route: pick up files, drop them on the
   destination folder in the tree. The folder highlights as you hover.
2. **Drag across the middle** onto the opposite contents column, which drops into whichever folder
   that side is showing.
3. **Drag onto a quick destination** — the pinned shortcuts along the top.
4. **Select, then press Move here** (or `M`). No dragging at all.

**Hold `Ctrl` while dropping to copy instead of move.** Or use the explicit **Copy here** button
(`C`).

## The queue

Sometimes you want to plan the whole reorganisation before anything happens. Press **Queue** (`Q`)
instead of *Move here* and the selection is staged: queued rows dim, the queue panel lists what is
waiting, and **nothing has touched the disk**.

Build up as many batches as you like — twelve files to Documents, eight to Photos, six to a project
folder — then press **Review & apply**. If you change your mind, remove an entry or clear the whole
queue and nothing has happened.

## When names clash

If any file would land on a name that already exists, Pineria stops **before moving anything** and
shows you exactly which ones clash, with the size of both the arriving and the existing file. You
choose once, for the whole batch:

| Choice | What actually happens |
| --- | --- |
| **Keep both** | The arriving file is renamed — `report.pdf` becomes `report (2).pdf`. Nothing existing is touched. This is the default because it cannot lose anything. |
| **Skip the clashes** | Files whose name is taken stay exactly where they are. Everything else still moves. |
| **Replace** | The file already at the destination is **sent to the Recycle Bin**, then replaced. Recoverable from Explorer, but it does change what is there. |

Even the most destructive option routes through the Recycle Bin. Pineria has no code path that
destroys a file outright.

## While it runs

A progress panel shows how far it has got, in files and in bytes, and which file is being handled
right now. Two controls:

- **Pause** stops between files — never in the middle of one — and **Resume** picks up where it
  stopped.
- **Stop after this file** cancels cleanly. What was already moved stays moved, and what had not
  been reached has not been touched.

If anything failed — a locked file, a permission problem, a disconnected drive — the panel lists the
failures with a plain explanation instead of silently skipping them. A failure on one file never
aborts the rest of the batch.

## Undo

**A batch of any size is a single `Ctrl+Z`.** Move 900 files and one undo puts all 900 back.

The full history is in `Ctrl+K` → *Show operation history*, where individual operations can be
undone out of order. Undoing a *copy* batch sends the copies it created to the Recycle Bin and
leaves your originals alone.

## If the app is interrupted mid-move

Before the first file moves, Pineria writes down everything it is about to do. So if the computer
crashes, the power fails, or the app is closed during a large batch, the next launch knows exactly
where it got to and shows you:

> **An organisation batch was interrupted.**
> 382 of 900 items were moved before it stopped.
> `Leave as is` · `Roll back` · `Finish the remaining 518`

- **Finish the remaining** completes only the files that had not been done.
- **Roll back** returns the files that *were* moved to where they came from.
- **Leave as is** keeps everything exactly where it currently sits and stops asking.

Nothing is decided for you, and nothing is lost while you decide.

## Plan mode

Sometimes you want to design the structure before you build it. Switch the right-hand side to
**Plan**.

Sketch a folder tree — add folders, add subfolders, rename, remove — and **none of it exists on
disk**. When you are satisfied, press **Create these folders** and Pineria builds the whole tree at
once. Folders that already exist are left alone.

Six starter templates are offered on an empty plan: a general archive, documents, photos by year,
projects, a media library, and software. Every one of them is fully editable — they are a starting
point, not a format.

> Plan mode creates folders. It does not move files into them; that is still your decision, made in
> Manual mode.

## Rules and suggestions

Switch the right-hand side to **Rules** to build simple matchers:

- extension is `pdf`
- name contains `invoice`
- kind is `image`
- larger than 100 MB
- older than 365 days

Each rule points at a destination folder. Press **Preview** and Pineria shows how many files each
rule would affect — **and stops there**. Matches go to the queue for you to approve.

**Rules never move anything by themselves.** Neither do suggestions. This is deliberate: automatic
classification was considered and rejected, because getting it wrong on someone's archive is worse
than not helping at all. Manual control is the primary mode, and the assistance is optional.

## Filters and search

Each side has its own search box and filter row.

Filters: **All**, **Unsorted**, Documents, Images, Videos, Audio, Archives, Code, **Large**,
**Recent**, **Old**, **Duplicates**.

**Unsorted** is the one worth knowing: it shows files sitting loose in a folder rather than filed
into one of its subfolders. That is your backlog. Work through it, and the folder is tidy by
definition.

In the search box, `*.pdf` filters by extension; anything else matches the name.

## Keyboard

| | |
| --- | --- |
| `M` | Move the selection to the other side |
| `C` | Copy it instead |
| `Q` | Add it to the queue |
| `Ctrl+A` | Select everything listed |
| `→` `←` | Expand and collapse a folder in the index |
| `Ctrl+B` | Show / hide the library sidebar |
| `Ctrl+P` | Show / hide the preview pane |
| `Ctrl+Z` | Undo the whole last batch |
| `F5` | Refresh both sides |
| `Escape` | Clear the selection |

---

## A worked example: taming Downloads

Say Downloads has four thousand files in it, going back years.

1. **Left side:** open Downloads. **Right side:** open where things should live.
2. Switch the right side to **Plan** and sketch the structure you want — `Documents`, `Media`,
   `Installers`, `Archive`. Press **Create these folders**, then switch back to **Manual**.
3. On the left, filter to **Documents**. Press `Ctrl+A`, then `Q` to queue them into your new
   `Documents` folder.
4. Repeat for **Images**, **Videos**, **Archives**, **Large**.
5. Glance at the queue: five batches, a few thousand files, nothing touched yet.
6. Press **Review & apply**. Answer the conflict dialog once if anything clashes. Watch it run.
7. Left side now shows what is left over — the genuinely miscellaneous. Filter to **Unsorted** and
   deal with what remains by hand.

If any of it was a mistake, `Ctrl+Z` per batch, in reverse order.
