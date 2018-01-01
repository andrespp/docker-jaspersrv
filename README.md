Docker JasperReports Server
===========================

# Introduction

DockerFile for JasperReports Server (https://sourceforge.net/projects/jasperserver/)

This image is based on `tomcat:9-jre8`.

JasperReports Server version on `latest` tag is `6.4.2`. Check `tags` for more recent image versions under development.

# Quick start

The easiest way to try this image is via docker compose:

```
version: '3.1'

services:
  jaspersrv:
    image: andrespp/jaspersrv
    restart: always
    ports:
      - "80:8080"
    depends_on:
      - jaspersrv-db
    environment:
      DB_TYPE: postgresql
      DB_HOST: jaspersrv-db
      DB_NAME: jasperdb
      DB_USER: jasperdb_user
      DB_PASSWORD: my-secret-password

  jaspersrv-db:
    image: postgres:10
    restart: always
    volumes:
     - ./data/pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: jasperdb
      POSTGRES_USER: jasperdb_user
      POSTGRES_PASSWORD: my-secret-password
```

Access it on `http://localhost/jasperserver` user/pass `jasperadmin/jasperadmin`.

On the first run, it is needed to seed the app's database. It can be done by running the command `seed`:

```
services:
  jaspersrv:
    image: andrespp/jaspersrv
    command: ["seed"]
    ...
```

# Environment variables

This image uses several environment variables in order to control its behavior, and some of them may be required

| Environment variable | Default value | Note |
| -------------------- | ------------- | -----|
| DB\_TYPE | postgresql | |
| DB\_HOST | localhost | |
| DB\_NAME | postgres | |
| DB\_USER | postgres | |
| DB\_PASSWORD| jasperserver | |

# Issues

If you have any problems with or questions about this image, please contact me
through a [GitHub issue](https://github.com/andrespp/docker-jaspersrv/issues).

