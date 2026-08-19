# Troubleshooting

[← Back to Pineria](../README.md)

Organised by what you are seeing. If your problem is not here, the
[FAQ](faq.md) covers the behaviour that surprises people most.

---

## Windows blocks the download or the app

**"Windows protected your PC"** or the browser refuses to keep the file.

Pineria is not code-signed, so Windows treats it as an unknown program. Click **More info** →
**Run anyway**. In some browsers you also have to choose *Keep* on the download.

If you would rather verify than trust, compare the hash against the `checksums.txt` in the release:

```powershell
Get-FileHash ".\Pineria.Setup.0.1.1.exe" -Algorithm SHA256
```

A matching hash means the file is exactly what was published. Only download from the
[official releases page](https://github.com/EnemyOfTheScorpion/pineria/releases).

## The app will not start

1. Confirm you are on 64-bit Windows 10 or 11.
2. Try the **portable** build. If that runs and the installed one does not, the installation is
   damaged — uninstall and reinstall.
3. Check whether antivirus quarantined it. Unsigned applications are sometimes removed silently;
   look in your antivirus's quarantine list and restore or allow it.
4. If it starts and immediately closes, the index may be damaged. Rename `%APPDATA%\Pineria\pineria.db`
   to `pineria.db.old` and start again — Pineria will build a new one. Your files are untouched;
   you would lose tags and collections, so [export them](faq.md#how-do-i-back-up-my-tags-and-collections)
   first if you can get the app open at all.

## A scan is slow, or looks stuck

Scanning reads every folder in the tree, so the time depends on the number of files and how fast the
disk is.

- **Network drives and NAS shares** are dramatically slower than local disks — every file needs a
  round trip. This is normal.
- **External drives** on USB 2.0 are slow in a way that looks like a hang.
- The status bar shows the file currently being read. If that path is changing, it is working.
- Stopping is always safe. What was already indexed stays usable, and the next scan continues from
  where it makes sense rather than starting over.

If the current path has not changed for several minutes, the folder is likely unreachable — a
disconnected drive or a share that has dropped. Stop the scan and check the drive.

## Search cannot find a file I know exists

Two causes, in order of likelihood:

**1. It has not been indexed yet.** The index only changes when a scan runs. Anything created,
renamed or moved outside Pineria is invisible until you rescan. Double-click the folder under
**Archive** in the sidebar, or `Ctrl+K` → *Scan all archive folders*.

**2. You are searching mid-word.** Matching starts at the beginning of a word. `roje` will never
find `project.pdf`; `proj` or `project` will. Names split on spaces and on `. _ - ( ) [ ] { } # @ + , ;`,
so `plan` does find `project-plan.pdf`.

Also check that the file is inside one of your archive folders at all, and that no filter chip is
still active from an earlier search.

## A folder shows the wrong file count

Counts in the Archive Organizer come from the index, so they reflect the last scan. Add or delete
files outside Pineria and the count is stale until you rescan that folder.

This is the intended behaviour, not a bug — but it is the most common thing people report, because
a wrong number looks broken.

## "Access denied" or permission errors on some folders

Windows protects parts of the disk, and some folders belong to other user accounts. Pineria skips
what it cannot read rather than failing the whole scan, so a scan that reports some folders as
unreadable is still valid for everything else.

Pineria also **refuses** to write into `Windows`, `Program Files`, `Program Files (x86)`,
`ProgramData` and drive roots, deliberately. That refusal is not a bug and cannot be overridden.

If a folder you own is denied, check its Properties → Security, or run the folder through Windows'
own "take ownership" flow. Pineria does not elevate itself.

## A file operation failed part of the way through

This is expected behaviour, not corruption: a failure on one file never aborts the rest of a batch.
The progress panel lists what failed and why.

Common causes: the file is open in another program, the destination drive filled up, or a drive
disconnected mid-operation.

Everything that succeeded is recorded as one operation, so `Ctrl+Z` reverses exactly that much.
Close whatever was holding the file and retry the remainder.

## A file went missing after a move

In this order:

1. **Check the history.** `Ctrl+K` → *Show operation history* shows every move, copy, rename and
   deletion with a timestamp and a count. It will tell you where the file went.
2. **Check the Recycle Bin.** If the file was deleted or displaced by a *Replace*, it is there.
3. **Check for a renamed copy.** If a name clashed and you chose *Keep both*, the file exists as
   `name (2).ext` at the destination.

Pineria has no code path that deletes a file permanently, so a file that was in the archive is in
one of those three places.

## The app was closed during a large move

Open the Archive Organizer. A banner at the top reports exactly how far the batch got and offers
three choices: **finish the remaining files**, **roll back** what was already done, or **leave as
is**.

Nothing is decided for you, and the offer stays until you answer it.

## Previews do not appear for some files

- Files larger than the preview limit are skipped. Raise it in **Settings → Appearance**.
- Video and audio stream regardless of that limit, but only formats Windows and the built-in player
  understand will play.
- Text previews show the first 512 KB of a file.
- Only ZIP archives are listed. Other archive formats are not read in this version.
- Preview can be turned off entirely in Settings — check that first if nothing previews at all.

## Everything feels slow in a very large folder

A folder with tens of thousands of files should still scroll smoothly, because only the rows on
screen are drawn. If it does not:

- Switch from **grid** to **list** view. Grid tiles come from the thumbnails Windows keeps, and are
  cached after the first look, but the first pass through a folder Windows has never drawn is the
  slow one.
- Close the preview pane with `Ctrl+P`.
- Use a filter or the search box to narrow the list rather than scrolling through everything.

## Reading the logs

**Settings → About → Open log folder**, or paste `%APPDATA%\Pineria\logs` into Explorer.

One plain-text file per day, the last seven kept. When Pineria shows an error it includes a short
id; searching the log for that id finds the technical detail behind it.

**Read a log before you share it.** It contains file paths from your machine, which may be private.
Deleting log files is harmless.

## Resetting Pineria completely

This removes the index, tags, collections, history and settings. **Your own files are not touched.**

1. Close Pineria.
2. Export your metadata first if you want to keep tags — **Settings → Backup → Export**.
3. Delete `%APPDATA%\Pineria`.
4. Start Pineria. It behaves like a fresh install, and you can re-add your archive folders.

## Reporting a problem

If none of the above helps,
[open a bug report](https://github.com/EnemyOfTheScorpion/pineria/issues/new?template=bug_report.yml).

Include the version (Settings → About), your Windows version, whether you used the installer or the
portable build, the steps that reproduce it, and any error id you were shown. Roughly how big the
archive is helps a great deal with anything slow.

If a file was lost or changed without being asked, say so in the title — those are looked at first.
Anything that risks other people's files should go through the
[private security form](https://github.com/EnemyOfTheScorpion/pineria/security/advisories/new)
instead.
