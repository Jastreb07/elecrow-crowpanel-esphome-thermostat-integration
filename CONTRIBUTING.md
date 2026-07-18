# Branching

Day-to-day work happens on **`dev`**, not `main`. `main` only receives
commits when `dev` is merged into it on purpose, right before a release.
This keeps `release-please` (below) from opening a release PR for every
small commit — it only reacts to what actually lands on `main`.

```powershell
git checkout dev
# ...commit, push to origin/dev as usual...

# When dev is ready to ship:
git checkout main
git merge dev
git push origin main
git checkout dev
```

# Releasing

This repo uses [release-please](https://github.com/googleapis/release-please)
to automate versioning and publishing on `main`. There is no manual version
bump or tagging step — it's driven entirely by commit messages.

## Commit message format

Use [Conventional Commits](https://www.conventionalcommits.org/) for
commits that end up on `main` (i.e. what you write on `dev` before
merging):

- `fix: ...` → patch release (`0.3.1` → `0.3.2`)
- `feat: ...` → minor release (`0.3.1` → `0.4.0`)
- `feat!: ...` or a `BREAKING CHANGE:` footer → major release (`0.3.1` → `1.0.0`)
- `docs:`, `chore:`, `refactor:`, `test:`, etc. → no release by themselves

## How a release happens

1. Merge `dev` into `main` and push, once `dev` is in a state you want to
   ship (see Branching above).
2. The `release-please` workflow opens or updates a **release PR** against
   `main` that bumps `manifest.json`'s `version`, updates `CHANGELOG.md`,
   and lists the included commits.
3. Merge that PR when you're ready to publish. This triggers a second run
   of the workflow that creates a Git tag and a GitHub Release.
4. HACS checks GitHub Releases (not just commits on `main`) to decide
   whether users have an update available, so this step is what actually
   makes a new version visible to HA users — nothing to do manually on the
   HACS side.

Users with HACS's "Automatic updates" setting enabled get it applied
automatically; everyone else sees an "Update available" notification in
HACS until they update manually. Neither this repo nor HACS can force an
update onto a user's Home Assistant instance.
