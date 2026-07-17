# docker_default

Local database dev environment via Docker Compose. No application code.

## Services

| Service     | Port  | Version            | Credentials                          |
|-------------|-------|--------------------|--------------------------------------|
| MySQL       | 55511 | 9.7                | root / 111111                        |
| phpMyAdmin  | 55512 | 5.2.3              | arbitrary server (point at host:55511) |
| MongoDB     | 55513 | 8.2                | admin / 111111 (`--auth` enabled)    |
| Redis       | 55514 | 8.8                | password: 111111                     |
| MariaDB     | 55516 | 12.3               | root / 111111                        |
| PostgreSQL  | 55515 | 18.4               | postgres / 111111                    |

## Commands

```sh
# Start all services
docker compose up -d

# Stop all services
docker compose down
```

## Notes

- Data directories (`db_mysql/`, `db_mongo/`, `db_mariadb/`, `db_postgres/`) are gitignored and auto-created on first start.
- Ports use the `555xx` range to avoid conflicts with host-native services.
- The `version` key in `docker-compose.yml` is obsolete but harmless.
- All passwords are hardcoded as `111111` — not for production use.
- MongoDB requires authentication (`--auth` flag); Redis requires `AUTH 111111` on connect.
- PostgreSQL 18+ requires volume mounted at `/var/lib/postgresql` (not `/var/lib/postgresql/data`) to allow version-specific subdirectory creation.
