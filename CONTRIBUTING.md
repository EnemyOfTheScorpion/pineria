# Contributing

[← Back to Pineria](README.md)

Thank you for wanting to help. This page is short and honest about what this repository is, so
nobody spends an evening on something that cannot be merged.

## What lives here

This repository is Pineria's public home: the documentation, the screenshots and the releases.
**The application's source code is not published.** Pineria is distributed as a compiled build
under the licence in [LICENSE](LICENSE), so there is no `src/` here to send a patch against.

That still leaves plenty that genuinely helps.

## The most useful thing you can do: report what broke

A good bug report is worth more than a guess at a fix.
[Open a bug report](https://github.com/EnemyOfTheScorpion/pineria/issues/new?template=bug_report.yml)
and include:

- **What you did, and what happened instead.** "Search returns nothing for a file I can see in the
  browser" beats "search is broken".
- **The version**, from **Settings → About**.
- **The error id** if Pineria showed one. Every error message carries a short id, and the same id is
  in the log — **Settings → About → Open log folder**, or `%APPDATA%\Pineria\logs`.
- **Whether it survives a restart**, and whether it happens on a different folder.

Please do not paste a log wholesale: it contains the paths of your own files. The lines around the
error id are enough, and you can edit anything private out of them.

## Something that risks your files, or anyone else's

Report it privately through the
[security advisory form](https://github.com/EnemyOfTheScorpion/pineria/security/advisories/new)
rather than in a public issue — see [SECURITY.md](SECURITY.md). That covers data loss as well as
security in the narrow sense: anything that could delete, overwrite or expose files.

## Documentation, which you *can* send a pull request for

Everything in `docs/`, the `README`, and this page are ordinary markdown in this repository, and
corrections are welcome — a step that no longer matches the app, a Windows detail that is wrong on
your machine, a sentence that reads as nonsense at eleven at night.

1. Fork, edit, and open a pull request against `main`.
2. Keep the existing voice: plain sentences, no marketing, no emoji headings, and a line width of
   about 100 characters.
3. Say in the pull request **which version you checked against** — the documentation describes a
   released build, not a plan.

Screenshots are welcome too, at the same window size as the ones in `assets/`, with no personal
paths or filenames visible.

## Ideas, questions, and "would you ever…"

[Discussions](https://github.com/EnemyOfTheScorpion/pineria/discussions) is the right place, and it
is a better place than an issue for anything that starts with "would you ever". Feature requests
that survive a conversation there tend to be much sharper by the time they become an issue.

Two things that will not be built, so you know before you write the post: **no telemetry or
analytics of any kind**, and **no cloud sync or account**. Both are structural promises, not
missing features.

## What happens after you post

This is a one-person project. Issues are read; they are not always answered quickly, and an issue
that stays open is not an issue that was ignored. Anything reported and then fixed is described in
the [changelog](CHANGELOG.md), in the release it went out in.
