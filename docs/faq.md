# FAQ

[← Back to Pineria](../README.md)

The questions people actually ask, answered directly.

---

## Is it really free? What is the catch?

It is free, and there is no catch. Every feature is available to everyone, at home and at work,
on as many machines as you like. There is no trial, no upgrade prompt, no advertising, and no data
being sold on the side — the application cannot send anything anywhere.

If it saves you an afternoon you can [sponsor the project](https://github.com/sponsors/EnemyOfTheScorpion),
but donations unlock nothing, because nothing is locked.

## Why does Windows warn me?

Because Pineria is not code-signed. A code-signing certificate costs several hundred dollars a year,
which a free application with no revenue does not have. Without one, Windows SmartScreen shows
*"Windows protected your PC"* for any new program it has not seen before.

To run it: click **More info**, then **Run anyway**.

If you would rather not take that on trust, verify the download instead. Every release publishes a
`checksums.txt`; compare it with:

```powershell
Get-FileHash ".\Pineria.Setup.0.1.0.exe" -Algorithm SHA256
```

If the hash matches, the file is byte-for-byte what was published. Only download Pineria from the
[official releases page](https://github.com/EnemyOfTheScorpion/pineria/releases) — copies hosted
elsewhere are not published by the maintainer.

## Does it work offline?

It only works offline. There is no online mode. Pineria has no network client at all, so there is
nothing to disconnect. See [Privacy](../PRIVACY.md).

## Does it upload my file names, or anything else?

No. No analytics, no crash reporting, no update check, no account. You can verify this with any
firewall or network monitor: scan, search and tag as much as you like and you will see no outbound
traffic.

## Does it move my files without asking?

No. Indexing is strictly read-only — a scan never copies, renames, moves or reorganises anything.
Files move only when you move them, and every move is recorded so it can be undone.

Suggestions and rules in the Archive Organizer only ever *propose*; they never act on their own.

## Can it delete something permanently?

No. Deletion goes to the Windows Recycle Bin, and there is no permanent-delete code path anywhere
in the application. That includes the "Replace" option when file names clash — the file being
replaced is sent to the Recycle Bin first, not destroyed.

Emptying the Recycle Bin is your decision, made in Windows.

## Where is my data stored?

In `%APPDATA%\Pineria` — the index, your tags and collections, the operation history, logs, and any
backups or exports you asked for. Paste that path into Explorer's address bar to open it.

Nothing is ever written next to your own files: no sidecar files, no hidden folders, no metadata
injected into your photos.

## Is the portable version really self-contained?

The *application* is: it installs nothing and leaves no Start Menu entries. But it still keeps its
index and settings in `%APPDATA%\Pineria`, like the installed version, so running it from a USB
stick on someone else's computer will leave that folder behind on their machine.

## Why doesn't search find matches in the middle of a word?

Because matching starts at a word boundary. `proj` finds `project-plan.pdf`; `roje` does not.

Names are split on spaces and on `. _ - ( ) [ ] { } # @ + , ;`, so `plan` does find
`project-plan.pdf` — it is a whole word there. Full mid-word matching would need a much larger index
and a slower search, and the trade-off was not judged worth it for file names.

## Why doesn't it find text inside my documents?

Pineria searches file names and paths, not file contents. It does not read the inside of your PDFs,
Word documents or spreadsheets, so it cannot search them. Content search is on the roadmap and is
not in this version.

## I just added a file and search cannot see it. Why?

Because the index only changes when a scan runs. There is no live filesystem watcher in this
version, so anything created, deleted or moved outside Pineria is invisible until the next scan.

Rescan a folder by double-clicking it under **Archive** in the sidebar, or run
`Ctrl+K → Scan all archive folders`.

## What happens to my tags if I move files in Explorer?

The tags stay in Pineria's database but lose their connection, because they are keyed by file path.
After the next scan the file appears at its new location with no tags.

Move files **inside** Pineria and the tags follow automatically — that is the main practical reason
to use the Archive Organizer rather than Explorer for reorganising.

## Does it work with a network drive or a NAS?

Yes, if the drive is mapped or reachable by UNC path. Expect scanning to be considerably slower than
a local disk, since every file needs a round trip over the network. If the share is unavailable when
you open Pineria, those entries stay in the index and are reported as missing by Archive health
until the drive is back.

## What about an external drive that is not always plugged in?

It works, with one caveat: while the drive is disconnected its files remain in the index, so they
appear in search results and the health report flags them as missing. Reconnect the drive and
rescan, and everything lines up again. Pineria never deletes index entries for a drive that is
merely absent.

## How large an archive can it handle?

Hundreds of thousands of files comfortably. The index is a description of your files, not the files
themselves, so a large archive means a database of tens of megabytes, not gigabytes.

A folder containing 12,000 files opens in about a second and stays smooth while scrolled, because
only the rows on screen are actually drawn.

## Does it slow my computer down?

Only while it is scanning, and even then the work happens on a background thread so the interface
stays responsive. There is no background service, no scheduled task, and nothing that starts with
Windows. When Pineria is closed it uses nothing at all.

## Is there a macOS or Linux version?

Not in this version, and not soon. The rules that protect your files — which folders are refused for
writing, how file names are validated, how deletion reaches the Recycle Bin — are written against
Windows. Shipping them elsewhere without rewriting them would mean protecting the wrong things.

## How do I update?

Download the latest release and install it over the top; your index, tags and collections are kept.
There is no auto-updater, which is a consequence of having no network client at all.

Watch the repository on GitHub to be notified of new releases.

## How do I back up my tags and collections?

**Settings → Backup**:

- **Export** writes your tags, collections, pins and settings to one JSON file. File contents are
  never included, so the export is small and portable between machines.
- **Import** merges an export back in. It never deletes anything.
- **Back up the database** takes a full copy of the index as well.

## What happens if it crashes while moving files?

The organiser writes down what it intends to do *before* it moves the first file. If the application
is interrupted, the next launch tells you exactly how far it got and offers three choices: finish
the remaining files, roll back what was already done, or leave everything as it is.

## How can I support the project?

Starring the repository genuinely helps other people find it. Reporting bugs clearly is worth more
than most people realise. And if you want to contribute financially,
[sponsorship is here](https://github.com/sponsors/EnemyOfTheScorpion) — entirely voluntary.
