# Zap-Database — releases

Installers for **[Zap-Database](https://github.com/JeremiePineau/zap-database)**, a cross-platform
desktop database client (PostgreSQL, Amazon Redshift, DuckDB).

The source lives in a private repository. This one exists so the Windows build can update itself:
electron-updater has to download the installer anonymously, and GitHub returns 404 for a private
repo's release assets without a token — which would mean shipping a credential inside every binary.
Splitting the artifacts out keeps the source private and the update feed publicly readable.

## Downloads

See **[Releases](https://github.com/JeremiePineau/zap-database-releases/releases)**. The `latest`
tag moves with every build.

- **Windows** — `Zap-Database-Setup-<version>.exe`. Updates itself from here; SmartScreen warns on
  first run because the build is unsigned.
- **macOS** — `Zap-Database-<version>-arm64.dmg` (Apple Silicon) or the x64 one. Ad-hoc signed but
  not notarized: open it once via System Settings → Privacy & Security → **Open Anyway**.
- **Linux** — `.AppImage` or `.deb`.

`latest.yml` is update metadata, not something to download by hand.

## Why the builds happen here

GitHub's standard runners are free on public repositories. On the private source repo the same
three-platform build bills at Linux 1×, Windows 2× and **macOS 10×**.

Only *packaging* runs here. Typechecking and tests stay on the private repo, because a failing
`tsc` or `vitest` prints several lines of real source around the failure, and a public repository's
logs are readable by anyone. The compile step's output is withheld on failure for the same reason.

The token this workflow uses is **read-only** on the source repo, and everything it publishes goes
to a release in this repository via the automatic `GITHUB_TOKEN` — so it cannot write to the
private one.
