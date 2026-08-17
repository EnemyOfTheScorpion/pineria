# Privacy

Short version: **Pineria makes no network connections at all.** Nothing you do in it leaves your
computer, because there is nothing in it that could send anything anywhere.

This page is deliberately specific, because "we respect your privacy" is what every application
says right before it uploads your file names.

---

## What Pineria sends

Nothing. There is no account system, no sync, no analytics, no crash reporting, no update check, no
"anonymous usage statistics", no advertising identifier.

The application contains no network client. Not a disabled one behind a setting — the code that
would make an outbound request does not exist in the build. The Settings screen shows telemetry as
*not implemented* rather than *off*, because that is the accurate word.

The only thing that ever reaches the internet is you, deliberately: clicking a link in the About
screen opens your normal browser, outside the application.

## What Pineria reads

Only the folders you nominate as archive roots, and only when you ask it to scan them.

For each file it records the things a file manager already shows you:

- its name, extension and full path
- its size
- when it was created, last modified and last accessed
- whether it is a file or a folder

**It does not read the contents of your files** during a scan. The only times a file's contents are
read at all are:

- when you select it and the preview pane draws it, and
- when you run a duplicate scan, which reads bytes in order to compare files — and even then it
  starts with sizes, so most files are never opened.

Some folders are skipped entirely: `$Recycle.Bin`, `System Volume Information`, and Windows'
recovery folders.

## What Pineria writes, and where

Everything it creates lives in one place inside your own user profile:

```
%APPDATA%\Pineria\
    pineria.db      the index, your tags, collections and history
    logs\           daily log files, kept for 7 days
    backups\        database backups, only when you ask for one
    exports\        metadata exports, only when you ask for one
```

**Nothing is ever written next to your own files.** No hidden `.pineria` folders, no sidecar files,
no metadata injected into your photos or documents. Your archive folders are left exactly as they
are unless you explicitly move, rename or create something.

Your tags and collections live in Pineria's database, keyed by file path. That is a deliberate
choice: your files stay ordinary files that any other program can open.

## Logs

Log files record what the application did — which folder was scanned, which operation failed and
why. They can contain file paths, because a path is usually the only useful thing to know when
something goes wrong.

Logs never leave your computer. Nothing uploads them, and Pineria never asks you to send them. If
you choose to attach one to a bug report, read it first — you can open the folder from
**Settings → About → Open log folder**.

## Removing everything

Uninstalling leaves `%APPDATA%\Pineria` in place on purpose, so reinstalling does not lose your tags
and collections. To remove every trace, delete that folder by hand after uninstalling.

Deleting it never touches your actual files — only Pineria's own index and settings.

## In short

| Question | Answer |
| --- | --- |
| Does it need an account? | No |
| Does it work offline? | It only works offline. It has no online mode. |
| Does it upload file names? | No |
| Does it read my documents? | Only to draw a preview you asked for, or to compare duplicates |
| Does it modify my files? | Only when you tell it to, and it can be undone |
| Can it delete something permanently? | No. Deletion goes to the Recycle Bin; there is no permanent-delete code path. |
| Where is my data? | `%APPDATA%\Pineria`, on your machine, and nowhere else |
