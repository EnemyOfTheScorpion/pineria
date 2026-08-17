# Installation

[← Back to Pineria](../README.md)

Everything about getting Pineria onto a machine, keeping it up to date, and taking it off again —
including the parts most installers do not tell you, like what survives an uninstall and where your
tags actually live.

---

## What it needs

| | |
| --- | --- |
| Operating system | Windows 10 or Windows 11, 64-bit |
| Disk space | About 250 MB for the application, plus the index |
| Anything else | **Nothing.** No runtime to install alongside it, no framework, no prerequisites |

The index grows with the *number* of files you have indexed, not their size. A few hundred thousand
files is a database measured in tens of megabytes, not gigabytes — Pineria stores a description of
your files, never the files themselves.

There is no macOS or Linux build. The rules that protect your files — which folders are refused for
writes, how names are validated, how deletion reaches the Recycle Bin — are written against Windows,
and shipping them elsewhere would mean protecting the wrong directories.

---

## Which download to choose

Every release has two executables. They are the same application.

| | `Pineria Setup 0.1.0.exe` | `Pineria Portable 0.1.0.exe` |
| --- | --- | --- |
| What it does | Installs Pineria properly | Runs straight from the file you downloaded |
| Administrator rights | Not needed — it installs for your user account only | Not needed |
| Shortcuts | Start Menu and desktop | None |
| Appears in Apps & features | Yes, with a working uninstaller | No |
| Where your index lives | `%APPDATA%\Pineria` | `%APPDATA%\Pineria` — the same place |

**Choose the installer** unless you have a specific reason not to. It puts the application somewhere
sensible, gives you shortcuts, and removes itself cleanly later.

**Choose the portable build** if you want to try Pineria without installing anything, or if you are
not allowed to install software on the machine.

### The portable build is portable in code, not in data

This one catches people out, so it is worth being blunt about it: **the portable build still writes
its database to `%APPDATA%\Pineria` on whatever computer you run it on.** Carrying the `.exe` on a
USB stick does not carry your tags and collections with it. Plug it into a different machine and you
get a fresh, empty index there.

If moving your work between computers is the goal, use the metadata export described further down.

---

## The SmartScreen warning

Pineria is not code-signed. A signing certificate costs several hundred dollars a year, which a free
application does not have. So the first time you run either executable, Windows will show a blue
box: *"Windows protected your PC"*.

That warning is honest. Windows is telling you it does not recognise the publisher, which is exactly
true.

To run it anyway:

1. Click **More info** in the warning box.
2. Click **Run anyway**.

You will see this once per new version. It is not a sign anything is wrong, and there is nothing to
disable.

### If you would rather not take it on trust

Every release ships a `checksums.txt` listing the SHA-256 fingerprint of each file. Download it
alongside the executable, then check the file you actually received:

```powershell
Get-FileHash ".\Pineria Setup 0.1.0.exe" -Algorithm SHA256
```

Or, to print just the fingerprint:

```powershell
(Get-FileHash ".\Pineria Setup 0.1.0.exe" -Algorithm SHA256).Hash
```

Compare the result against the matching line in `checksums.txt`. Capitalisation does not matter; the
characters do. If they match, the file you have is byte-for-byte the file that was published.

If they **do not** match, delete the download and fetch it again. Do not run it. A mismatch usually
means an interrupted download, but there is no way to tell that apart from the alternative, so treat
it as the alternative.

---

## Installing

Run `Pineria Setup 0.1.0.exe` and follow the two or three prompts. There is no administrator prompt,
because Pineria installs for your user account only.

By default it goes to:

```
%LOCALAPPDATA%\Programs\Pineria
```

You can change that during setup if you prefer somewhere else. The installer creates a Start Menu
entry and a desktop shortcut, both called **Pineria**, and registers an uninstall entry so it shows
up in Windows Settings like any other application.

That is the whole install. Nothing runs in the background, nothing is scheduled, and nothing starts
with Windows.

### The first run

The first time Pineria opens, it asks you to choose one folder to index — an archive root. Pick a
folder you actually care about rather than a whole drive, and the scan starts in the background
while you look around.

Scanning is read-only. It records names, paths, sizes and dates into Pineria's own database. It does
not create sidecar files, hidden folders or thumbnail caches inside your folders, and it never moves
anything. [Quick start](quick-start.md) walks through the first ten minutes.

### Running the portable build

Put `Pineria Portable 0.1.0.exe` wherever you like and double-click it. It unpacks itself and runs.
There is nothing to install and no shortcut to create — make one by hand if you want one.

Only one copy of Pineria runs at a time, installed or portable. Launching a second copy brings the
first window to the front instead of opening a second one, because two copies must never write to
the same database at once.

---

## Where your data lives

Everything Pineria creates sits in one folder:

```
%APPDATA%\Pineria\
├─ pineria.db     your index, tags, collections, pins, settings and history
├─ logs\          one plain-text file per day, the 7 newest kept
├─ backups\       database backups you asked for — never deleted automatically
└─ exports\       metadata exports, when you do not pick a save location
```

`%APPDATA%` expands to `C:\Users\<you>\AppData\Roaming`. Paste the path above into the Explorer
address bar to open it, or find the exact locations in Settings → About.

A few things worth knowing:

- **`pineria.db` is the only file that matters.** It holds everything you have built by hand.
- You may see two small companion files sitting next to it while Pineria is running. Leave them
  alone. If you want a copy of the database, use the backup button in Settings → Backup rather than
  copying the file yourself — that way the copy is guaranteed to be complete.
- **Logs contain the full paths of files being processed.** They are ordinary text and they stay on
  your machine, but read one before attaching it to a bug report.
- **Backups are never pruned.** Logs clean themselves up after seven days; backups accumulate until
  you delete them.

Nothing is ever written next to your own files. See [Privacy](../PRIVACY.md) for the complete
account of what Pineria reads and writes.

---

## Updating

There is no auto-updater, and no update check. Pineria never contacts anything.

To update: download the newer release and install it over the top of the old one. You do not need to
uninstall first. Your database is untouched by the upgrade, so your index, tags and collections are
exactly where you left them when the new version opens.

For the portable build, replace the old `.exe` with the new one and delete the old file.

---

## Uninstalling

**Installed build.** Windows Settings → Apps → Installed apps → **Pineria** → Uninstall. Or use the
uninstall entry in the Start Menu. This removes the program files and the shortcuts.

**Portable build.** Delete the `.exe`. There is nothing else on the program side to remove.

### What is deliberately left behind

Uninstalling does **not** delete `%APPDATA%\Pineria`.

That is a decision, not an oversight. Your tags, collections and settings are work you did by hand,
sometimes over months, and an uninstaller has no business destroying it. Reinstall Pineria later and
everything is still there.

Your indexed files are, of course, completely untouched. Pineria only ever held a description of
them — removing it removes the description, not the archive.

### Removing every trace

If you want Pineria gone entirely:

1. Uninstall it, or delete the portable `.exe`.
2. Delete `%APPDATA%\Pineria` yourself.

That is all of it. Nothing is left in `%ProgramData%`, nothing runs as a service or a scheduled
task, and the only registry entry is the standard per-user uninstall record that Windows uses to
list the app — removed by the uninstaller.

If there is any chance you will come back, export your metadata to somewhere outside `%APPDATA%`
before you delete the folder.

---

## Moving to a new computer

You cannot usefully copy the database across, because it is a description of one particular
machine's folders. What travels is your **metadata export**: a single JSON file holding your tags
and which files carry them, your collections and their contents, your pinned folders, your archive
root paths and your settings. No file contents, no index.

On the old machine:

1. Settings → Backup → export metadata.
2. Save the JSON file somewhere you will still have it — not inside `%APPDATA%`.

On the new machine:

1. Install Pineria.
2. Settings → Backup → import that JSON file.
3. Add your archive folders and run a scan.

Import merges. It adds what is missing and never deletes anything you already have, so importing
twice is harmless. Three things to know before you press it:

- **Import overwrites your current settings** with the ones stored in the file.
- **Import does not start a scan.** It registers your archive folders, but nothing is searchable
  until you scan them.
- **Tags are matched by full path.** If your archive lived at `D:\Photos` on the old machine and
  lives at `E:\Archive\Photos` on the new one, the imported tags will point at paths that do not
  exist there, and they will not attach to anything. Same drive letter and same folder layout means
  everything lands where it should.

The export is plain, readable JSON, so if the paths did change, it is possible to open it in a text
editor and correct them before importing.

---

## Next

- [Quick start](quick-start.md) — your first ten minutes
- [Features](features.md) — what everything does, and where the limits are
- [Troubleshooting](troubleshooting.md) — when something goes wrong
- [FAQ](faq.md) — the questions people actually ask
