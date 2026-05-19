# Activity 1.02 — Accessing the PostgreSQL Database

## Command
docker exec -it my-postgres psql -U docker mydb

## Inside psql
\l    -- list databases
\q    -- quit

## Key Observations
- docker exec -it = run interactive command inside running container
- No need to pass credentials again — container already has them from -e flags
- mydb database created automatically via POSTGRES_DB env var
- psql version: 17.10 (Debian)
- 4 databases present: mydb, postgres, template0, template1

## 2026 Notes
- docker exec is primary tool for debugging running containers
- Never use docker attach for database containers — use exec instead
