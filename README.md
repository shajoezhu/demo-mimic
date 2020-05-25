# demo-mimic

This repo is a git-sparse-checkout from https://github.com/MIT-LCP/mimic-code

## Repo structure

```
  /   # Root
  |-- data     # mimic-demo data
  |-- postgres # scripts for SQL database
  |-- docker   # Dockerfile etc
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

```bash
docker build . -f docker/Dockerfile -t shajoezhu/demo-mimic
```

Or you can pull it from docker repository via

```bash
docker pull shajoezhu/demo-mimic
```

### Deployment

For the first time, we need to build the database

```bash
docker run -d \
--name demo-mimic-container \
-p 5433:5432 \
-e POSTGRES_PASSWORD=postgres \
-e MIMIC_PASSWORD=mimic \
-e BUILD_MIMIC=1 \
demo-mimic
```

#### Stop deployment

```bash
docker stop demo-mimic-container
```

#### Restart deployment

```bash
docker start demo-mimic-container
```
