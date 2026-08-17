# Quick start

[← Back to Pineria](../README.md)

Your first ten minutes with Pineria. By the end of it you will have an archive indexed, you will
have found something in it, and you will have tidied one messy folder.

Nothing in this guide moves, renames or deletes a file unless the step says so explicitly.

---

## 1. First run

Open Pineria. You are greeted by three short cards — read them or press **Skip**, it makes no
difference to anything.

Then choose your first archive folder. Pick something real but not enormous for the first go: your
Downloads folder, or one drive of photos. You can add more later, and you can remove one without
losing anything.

**What happens next:** Pineria walks the folder and records what it finds. This is read-only. It
does not copy, rename or reorganise anything, and it never writes into the folder it is reading.

You can keep using the app while it works. The status bar at the bottom shows live progress and a
**Stop** button — stopping is safe, and what was already indexed stays usable.

![Browsing an indexed folder with the preview pane open](../assets/browse.png)

A first scan of a few thousand files takes seconds. A hundred thousand takes a couple of minutes.

---

## 2. Find something · `Ctrl+F`

Type into the search box at the top. Results appear as you press Enter.

![Search results, with tags shown on the cards](../assets/search.png)

Two things are worth knowing straight away, because they explain almost every "why can't it find
my file" moment:

- **Matching starts at the beginning of a word.** `proj` finds `project-plan.pdf`. `roje` finds
  nothing.
- **It searches names and paths, not the text inside your documents.** Searching `invoice` finds
  `invoice-2026.pdf`; it will not find a PDF that merely contains the word.

Narrow results with the filter chips that appear under the search box: file type, size, date, and
the extensions that are actually common in *your* archive. Click **In this folder** to restrict a
search to wherever you were browsing.

---

## 3. Tag a few files · `T`

Select some files — click, then `Ctrl+click` to add, or `Shift+click` for a range — and press `T`.

Type a name and press **Add**. That is a tag: a label that lives alongside your folders instead of
fighting them. A file can carry as many as you like, and one tag can span twenty different drives.

Tags appear in the left sidebar with a count. Click one to see everything carrying it. Right-click
one to rename it, change its colour, or delete it — deleting a tag removes the label and never
touches a file.

**Tags follow your files** when you move or rename them *inside* Pineria. If you move a file in
Windows Explorer instead, Pineria loses track of it until the next scan.

---

## 4. See what you actually have · Overview

Click **Overview** in the left rail.

![The archive overview](../assets/dashboard.png)

This is the answer to "what is even in there": how many files and folders, how much space, the
split by type, your largest files, what changed recently, and — once you have run a duplicate scan
— how much space duplicates are wasting.

---

## 5. Find duplicates · Copies

Click **Copies**, choose a minimum size, and press **Scan for duplicates**.

Pineria compares file sizes first, so most of your archive is never read from disk at all. Only
files that are the same size get fingerprinted, and only files with matching fingerprints get read
in full. That is why it finishes in seconds rather than hours.

What you get is a list of groups of genuinely identical files, with the reclaimable space for each.
**Nothing is deleted for you.** Pick which copy to keep, and *Bin the others* sends the rest to the
Windows Recycle Bin, where they stay until you empty it.

---

## 6. Tidy one folder · Organise

This is the part most people came for. Click **Organise** in the left rail.

The screen splits into four columns: your folder structure on the far left, its contents next to it,
then the contents of wherever you want files to end up, and that destination's structure on the far
right. The two middle columns face each other, so moving a file is a short drag across the middle.

Try this:

1. On the left, pick a messy folder — Downloads is the classic.
2. On the right, navigate to where things should live. Need a new folder? Press the **+** in the
   right-hand column's header.
3. Select some files on the left. `Ctrl+A` takes everything currently listed.
4. Either drag them across, or press **Move here**.

If any names clash, Pineria stops and asks before touching anything. Everything you just did is
**one** `Ctrl+Z`, however many files were involved.

Not ready to commit? Press **Queue** instead of *Move here*. Queued work is staged and touches
nothing until you press *Review & apply*, so you can plan the whole reorganisation first and run it
in one go.

[The full guide to the Organiser →](archive-organizer.md)

---

## Worth knowing on day one

- **`Ctrl+K`** opens the command palette. Everything the app can do is in there, searchable. If you
  learn one shortcut, learn this one.
- **The index updates when you scan**, not the moment a file changes. If you add files outside
  Pineria, rescan the folder (double-click it under **Archive** in the sidebar) to see them.
- **Undo is real.** `Ctrl+Z` reverses moves, renames, folder creation and tagging. The one exception
  is the Recycle Bin — Windows owns that, so you restore from Explorer.
- **Nothing you do here needs an internet connection**, and nothing about your files leaves the
  machine. See [Privacy](../PRIVACY.md).

## Where to go next

- [Features](features.md) — everything the app does, and where each limit sits
- [Archive Organizer](archive-organizer.md) — the reorganisation workspace in depth
- [FAQ](faq.md) — the questions people actually ask
- [Troubleshooting](troubleshooting.md) — when something looks wrong
