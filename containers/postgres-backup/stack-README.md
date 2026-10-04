# Initial Deployment Requirements
## Prerequisites for using postgres-backup

# Create and Setup Required Folders
## Restore from a dump

List available dumps (daily/weekly/monthly subfolders, gzip-compressed SQL):

```bash
docker exec -it ${projectName}-postgres-backup ls -la /backups
```

Restore into a *scratch* postgres instance first, never directly into the live one, to confirm the dump is actually valid before trusting it:

```bash
gunzip -c /opt/docker/volumes/$projectName/postgres-backup-data/daily/<dump-file>.sql.gz \
  | docker exec -i <scratch-postgres-container> psql -U <user> -d <db>
```

| Placeholder | Value |
| --- | --- |
| `<dump-file>` | The dump's name without `.sql.gz`, from the list above |
| `<scratch-postgres-container>` | The scratch Postgres container to restore into |
| `<user>` | The database user, such as `komodo-admin` |
| `<db>` | The database to restore into |
