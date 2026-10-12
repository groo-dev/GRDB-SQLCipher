# GRDB + SQLCipher (Space fork)

This is [GRDB.swift](https://github.com/groue/GRDB.swift) **v7.11.1** with GRDB's own
documented `GRDB+SQLCipher` recipe enabled in `Package.swift`, and nothing else changed.

Changes versus upstream (one commit on branch `sqlcipher`):
- depends on Zetetic's [SQLCipher.swift](https://github.com/sqlcipher/SQLCipher.swift) (`from: "4.11.0"`);
- defines `SQLITE_HAS_CODEC` (C and Swift) and `SQLCipher` (Swift);
- removes the `GRDBSQLite` system-library product/target; adds the `GRDBSQLCipher` target.

Used by Space's iOS `SpaceStore` framework (encrypted offline mail). SpaceStore links this
as the ONLY GRDB importer, behind a dynamic framework boundary, so every SQLite call binds to
SQLCipher (see Space's spike findings).

## Rebasing on a new GRDB release

```bash
git fetch https://github.com/groue/GRDB.swift.git --tags
git switch -c sqlcipher-X.Y.Z vX.Y.Z
git cherry-pick <this fork's recipe commit>   # re-apply the Package.swift recipe
swift build
git tag vX.Y.Z-sqlcipher.1
```

Tags: `vX.Y.Z-sqlcipher.N` (pin with `exact:`).
