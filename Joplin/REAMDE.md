# Introduction
## docker-compose.yml
```
version: '3'

services:
    db:
        image: postgres:15
        volumes:
            - ./joplindb:/var/lib/postgresql/data
        restart: unless-stopped
        env_file: .env
    app:
        image: joplin/server:latest
        depends_on:
            - db
        ports:
            - "9016:22300"
        restart: unless-stopped
        env_file: .env
```
## .env
Set your environment variables. SMTP details are optional if you want Mealie to be able to send emails.

```
# GENERAL
APP_PORT=22300
APP_BASE_URL=https://yourdomain
# Database configuration
#
# Optional: 'sqlite', 'pg'
DB_CLIENT=pg
POSTGRES_PASSWORD=joplin
POSTGRES_DATABASE=joplin
POSTGRES_USER=joplin
POSTGRES_PORT=5432
POSTGRES_HOST=db
# E-mail configuration
#
# all required if SMTP_AUTH_STRATEGY is 'TLS' or 'SSL'
MAILER_ENABLED=1
MAILER_HOST=yourdomain
MAILER_PORT=587
MAILER_SECURE=1
MAILER_AUTH_USER=Joplin
MAILER_AUTH_PASSWORD=Joplin
MAILER_NOREPLY_NAME=Joplin
MAILER_NOREPLY_EMAIL=youremail
```

## Startup

```
docker-compose up -d
```