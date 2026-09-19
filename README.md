# Perfection à la Carte — Cook Studio

Cook one dish twice — once rushed against a timer, once slow with unlimited time — and
turn the session into an Instagram carousel. No accounts, no server: everything lives
in your phone's browser storage.

## Files

- `index.html` — the entire app (UI + logic)
- `versions/` — one full snapshot per version, for rollback
- `CHANGELOG.md` — what changed in each version
- `serve.ps1` — local dev server only, do **not** upload

## Version history

Real git history — every design revision is a commit. See `git log` for the full list.

Full notes per version: [CHANGELOG.md](CHANGELOG.md). Every version is also a complete
snapshot in `versions/index-vX.Y.html` — current is **v3.0**.

**Roll back** (no git needed): copy the snapshot you want over `index.html`, e.g.
```powershell
Copy-Item versions\index-v2.2.html index.html
```
Then re-upload `index.html` to GitHub (step 2 below) to publish the rollback.

**See what changed between versions:**
```powershell
git log --oneline          # list all versions
git show <commit-hash>     # see exactly what changed in that version
```

## Publish (one-time, ~5 minutes, free)

Voice recording requires HTTPS. Easiest path — GitHub Pages:

1. Go to https://github.com/new → repository name `cook-studio` → **Public** → Create.
2. On the empty repo page, click **uploading an existing file** and drag in `index.html`. Commit.
3. Repo **Settings → Pages** → under "Branch" choose `main` and `/ (root)` → Save.
4. After ~1 minute your app is live at `https://kissie-source.github.io/cook-studio/`.

## Install on your phone (one-time)

1. Open the URL above in Chrome (Android) or Safari (iPhone).
2. **iPhone:** Share button → Add to Home Screen. **Android:** ⋮ menu → Add to Home screen.
3. First recording/photo asks for mic/camera permission — Allow.

## Updating the app

When a new version is ready: this repo's `index.html` gets the change and a new commit.
Re-upload that `index.html` to your GitHub repo (same drag-and-drop as step 2) to push
the update live. Your phone picks it up next time you open the app.
