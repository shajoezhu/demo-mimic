# mimic-postgres

To build the database

```bash
psql -U postgres -c "alter user postgres superuser;"
createdb postgres
make create-user
make mimic-gz datadir="data"
```

To test

```bash
psql "dbname=mimic user=postgres password=postgres options=--search_path=mimiciii" -v ON_ERROR_STOP=1 -f postgres_checks.sql
```
