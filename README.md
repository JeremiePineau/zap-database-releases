# Zap-Database — releases

Installers for **[Zap-Database](https://github.com/JeremiePineau/zap-database)**, a cross-platform
desktop database client (PostgreSQL, Amazon Redshift, DuckDB).

The source lives in a private repository. This one exists so the Windows build can update itself:
electron-updater has to download the installer anonymously, and GitHub returns 404 for a private
repo's release assets without a token — which would mean shipping a credential inside every binary.
Splitting the artifacts out keeps the source private and the update feed publicly readable.

## Downloads

See **[Releases](https://github.com/JeremiePineau/zap-database-releases/releases)**. The `latest`
tag moves with every build from `master`.

- **Windows** — `Zap-Database.Setup.<version>.exe`. Updates itself from here; SmartScreen warns on
  first run because the build is unsigned.
- **macOS / Linux** — attached to the private source repo's releases instead.

`latest.yml` is update metadata, not something to download by hand.
