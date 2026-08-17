# Security

Pineria manages people's files. A bug that loses a file matters as much as one that leaks data, and
both are treated as security issues here.

## Reporting

**Please do not open a public issue for anything in this list.**

Report it privately through
[GitHub's security advisory form](https://github.com/EnemyOfTheScorpion/pineria/security/advisories/new).
It is private between you and the maintainer until a fix ships.

Report privately if you find a way to make Pineria:

- delete, overwrite or corrupt a file the user did not ask it to touch
- write outside the folders the user chose, or into a protected Windows location
- escape the path guards (traversal, junction or symlink tricks, crafted file names)
- execute something, load code from a file it previewed, or make any network request
- expose the contents of files the user did not open

For anything else — a crash, a slow scan, a layout problem, a wrong count — a normal
[bug report](https://github.com/EnemyOfTheScorpion/pineria/issues/new?template=bug_report.yml)
is the right place, and public discussion helps other people.

### What to include

The version, your Windows version, and the smallest sequence of steps that reproduces it. If it
involves a specific file name or folder structure, describe the shape of it rather than sending
real files.

You will get an acknowledgement within a few days. Pineria is maintained by one person, so please
allow reasonable time for a fix before disclosing publicly.

## Supported versions

Only the latest release. There are no long-term support branches.

| Version | Supported |
| --- | --- |
| 0.1.x | ✅ |
| older | ❌ |

## How Pineria is built to fail safely

Useful context when judging whether something is a real problem:

- **Deletion is Recycle Bin only.** There is no permanent-delete code path in the application. Even
  an explicit "replace this file" sends the displaced file to the Recycle Bin first.
- **Transfers never overwrite silently.** A name collision becomes `name (2).ext` unless you
  explicitly choose otherwise, and you are shown the clashes before anything moves.
- **Protected locations are refused.** Drive roots, `Windows`, `Program Files`,
  `Program Files (x86)` and `ProgramData` are rejected for every write, whatever asked for it.
- **Large operations are journalled.** A batch writes its intent to disk before the first file
  moves, so a crash leaves a recoverable record rather than an unknown half-state.
- **Everything is undoable**, apart from the Recycle Bin itself, which Windows owns.
- **No network client exists**, so there is no remote attack surface. The only inputs are the
  files you point it at.

## Not code-signed

Releases are not signed with a code-signing certificate, so Windows SmartScreen warns on first run.
This means you cannot rely on the signature to prove a download is genuine — **verify the SHA-256
checksum** published with each release instead.

Only ever download Pineria from
[this repository's Releases page](https://github.com/EnemyOfTheScorpion/pineria/releases). Copies
hosted anywhere else are not published by the maintainer and should not be trusted.
