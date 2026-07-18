# Releasing

This repo uses [release-please](https://github.com/googleapis/release-please)
to automate versioning and publishing. There is no manual version bump or
tagging step — it's driven entirely by commit messages on `main`.

## Commit message format

Use [Conventional Commits](https://www.conventionalcommits.org/):

- `fix: ...` → patch release (`0.3.1` → `0.3.2`)
- `feat: ...` → minor release (`0.3.1` → `0.4.0`)
- `feat!: ...` or a `BREAKING CHANGE:` footer → major release (`0.3.1` → `1.0.0`)
- `docs:`, `chore:`, `refactor:`, `test:`, etc. → no release by themselves

## How a release happens

1. Push Conventional Commits to `main` (directly or via merged PR).
2. The `release-please` workflow opens or updates a **release PR** that
   bumps `manifest.json`'s `version`, updates `CHANGELOG.md`, and lists the
   included commits.
3. Merge that PR when you're ready to ship. This triggers a second run of
   the workflow that creates a Git tag and a GitHub Release.
4. HACS checks GitHub Releases (not just commits on `main`) to decide
   whether users have an update available, so this step is what actually
   makes a new version visible to HA users — nothing to do manually on the
   HACS side.

Users with HACS's "Automatic updates" setting enabled get it applied
automatically; everyone else sees an "Update available" notification in
HACS until they update manually. Neither this repo nor HACS can force an
update onto a user's Home Assistant instance.
