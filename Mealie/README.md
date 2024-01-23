# Introduction
## docker-compose.yml
```
---
services:

  mealie:
    image: hkotel/mealie
    container_name: mealie-app
    hostname: mealie
    restart: always
    env_file: .env
    ports:
      - "9012:9000"
    # depends_on:
    #   - postgres
    volumes:
      - ./mealie_data/:/app/data
  # postgres:
  #   container_name: mealie-db
  #   image: postgres:15
    # restart: always
  #   volumes:
  #     - ./mealie_pgdata:/var/lib/postgresql/data
networks:
  default:
    name: $DOCKER_MY_NETWORK
    external: true
```
## .env
Set your environment variables. SMTP details are optional if you want Mealie to be able to send emails.

```
# GENERAL
DOCKER_MY_NETWORK=yournetwork
TZ=Europe/Berlin

# MEALIE
PUID=1026
PGID=100
DEFAULT_GROUP=[nuz:y]
# DEFAULT_USER=yourname
BASE_URL=http://localhost:9012

# Allow user sign-up without token | true or false
ALLOW_SIGNUP=true
API_DOCS=true
#TOKEN_TIME=48
RECIPE_PUBLIC=true
RECIPE_SHOW_NUTRITION=true
RECIPE_SHOW_ASSETS=true
RECIPE_LANDSCAPE_VIEW=true
RECIPE_DISABLE_COMMENTS=false
RECIPE_DISABLE_AMOUNT=false

# Security
#
# Maximum times a user can provide an invalid password before their account is locked | default 5
SECURITY_MAX_LOGIN_ATTEMPTS=5
# Time in hours for how long a users account is locked | default 24
SECURITY_USER_LOCKOUT_TIME=24

# Database configuration
#
# Optional: 'sqlite', 'postgres'
DB_ENGINE=sqlite
# postgres configuration
# POSTGRES_USER=mealie
# POSTGRES_PASSWORD=yourpassword
# POSTGRES_SERVER=postgres
# POSTGRES_PORT= 5432
# POSTGRES_DB=mealie

# E-mail configuration
#
# all required if SMTP_AUTH_STRATEGY is 'TLS' or 'SSL'
# SMTP_HOST=
# SMTP_PORT=
# SMTP_FROM_NAME=
# SMTP_AUTH_STRATEGY=TLS
# SMTP_FROM_EMAIL=
# SMTP_USER=
# SMTP_PASSWORD=

# Webworker configuration
#
# Changing the webworker settings may cause unforeseen memory leak issues 
# with Mealie. It's best to leave these at the defaults unless you begin 
# to experience issues with multiple users. Exercise caution when 
# changing these settings

# Enables Gunicorn to manage Uvicorn web for multiple works
#WEB_GUNICORN=false

# Set the number of workers to the number of CPU cores multiplied by 
# this value (Value * CPUs).
#WORKERS_PER_CORE=1

# Set the maximum number of workers to use. Default is not set 
# meaning unlimited.
#MAX_WORKERS=1

# Override the automatic definition of number of workers.
#WEB_CONCURRENCY=1
```

## Startup

```
docker-compose up -d
```