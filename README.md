# mimic-postgres

## Repo structure

```
  /
  |-- data
  |-- postgres
  |-- docker
```

## To build the database with postgres

### Build

```bash
cd postgres
psql -U postgres -c "alter user postgres superuser;"
createdb postgres
make create-user
make mimic-gz datadir="../data"
```

### Test

```bash
psql "dbname=mimic user=postgres password=postgres options=--search_path=mimiciii" -v ON_ERROR_STOP=1 -f postgres_checks.sql
```

## To build the database with docker

### Build
