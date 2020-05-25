# demo-mimic

This repo is a git-sparse-checkout from https://github.com/MIT-LCP/mimic-code

## Repo文件结构 (Repo structure)

```
  /   # Root
  |-- data     # mimic-demo data
  |-- postgres # scripts for SQL database
  |-- docker   # Dockerfile etc
```

## SQL数据库构建 (Build the database with postgres)

### 构建数据库 (Build)

```bash
cd postgres
psql -U postgres -c "alter user postgres superuser;"
createdb postgres
make create-user
make mimic-gz datadir="../data"
```

### 测试链接 (Test)

```bash
psql "dbname=mimic user=postgres password=postgres options=--search_path=mimiciii" -v ON_ERROR_STOP=1 -f postgres_checks.sql
```

## 用docker构建数据库 (Build the database with docker)

### 构建数据库

```bash
docker build . -f docker/Dockerfile -t shajoezhu/demo-mimic
```

或者直接从docker库下载 (Or you can pull it from docker repository via)

```bash
docker pull shajoezhu/demo-mimic
```

### Docker部署 (Deployment)

首次运行,需要组建数据库 (For the first time, we need to build the database)

```bash
docker run -d \
--name demo-mimic-container \
-p 5433:5432 \
-e POSTGRES_PASSWORD=postgres \
-e MIMIC_PASSWORD=mimic \
-e BUILD_MIMIC=1 \
demo-mimic
```

#### 停止Docker部署 (Stop deployment)

```bash
docker stop demo-mimic-container
```

#### 重启Docker部署 (Restart deployment)

```bash
docker start demo-mimic-container
```
