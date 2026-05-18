# Exercise 1.02 — Managing Container Life Cycles

## Commands
docker run -d nginx
docker container pause <id>
docker container unpause <id>
docker container stop <id>
docker container rm <id>

## Key Observations
- Detached mode (-d) returns container ID immediately
- Pause = cgroups freezer (SIGSTOP equivalent) — memory preserved, zero CPU
- Stop = SIGTERM → 10s grace period → SIGKILL if needed
- rm deletes container layer, image remains on disk
- Stopped containers still appear in `ls -a` until explicitly removed

## 2026 Notes
- Use --rm flag on short-lived containers to auto-remove on exit
- `docker container stop` default timeout is 10s (use -t to change)
