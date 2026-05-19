# Activity 1.01 — Running a PostgreSQL Container

## Final Command
docker run -d \
  --name my-postgres \
  -e POSTGRES_USER=docker \
  -e POSTGRES_PASSWORD=docker \
  -e POSTGRES_DB=mydb \
  postgres:17

## Key Observations
- -d = detached mode, runs in background
- --name = named container, avoid random names
- -e = environment variable injection (like export on Linux)
- POSTGRES_PASSWORD is mandatory — container refuses to start without it
- Confirmed healthy via: "database system is ready to accept connections"
- docker exec <container> env — inspect env vars inside running container

## 2026 Notes
- Book uses postgres:12 — EOL since Nov 2024, use postgres:17
- Never hardcode passwords in run commands in production — use Docker secrets or env files
