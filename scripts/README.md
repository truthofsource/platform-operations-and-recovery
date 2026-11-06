# PostgreSQL backup and restore patterns

These three scripts adapt the author's operational PostgreSQL backup/rehearsal implementation, with neutral naming and no environment identifiers. Unlike the SQLite dashboard, they operate on real local Docker containers and can upload through AzCopy when explicitly enabled.

- `snapshot_cluster.py`: capture database/table row counts without printing row values. Application database names must start with `platform`.
- `backup-postgres.sh`: requires `ALLOW_CLOUD_BACKUP=true` and `PLATFORM_BACKUP_CONTAINER_URL`; uses managed-identity AzCopy, omits role passwords, uploads dump/checksum/inventory without overwrite. Run only on an approved host.
- `check-restore.sh`: requires `PLATFORM_RESTORE_POSTGRES_IMAGE=postgres@sha256:<reviewed digest>`. Validates gzip and checksum, restores in a unique disposable `--network none` container and optionally compares inventory. No host port is exposed. Trust auth is confined to that isolated disposable container.

```bash
# An existing approved dump is required; this does not create a cloud backup.
export PLATFORM_RESTORE_POSTGRES_IMAGE='postgres@sha256:<reviewed-digest>'
bash scripts/check-restore.sh dump.sql.gz dump.sql.gz.sha256 expected.inventory.json
```

The checksum sidecar and inventory must come from a trusted protected archive. A checksum stored beside an attacker-modified backup is not an authenticity signature. Take inventory and dump during a consistent snapshot or quiesced application window; separate queries while writers run can disagree. Validate database compatibility and role recreation separately. No real cloud upload or PostgreSQL recovery is claimed by the default local-demo screenshot.
