# Exercise 1.01 — Running the hello-world Container

## Commands
```bash
docker run hello-world
docker container ls -a
docker image ls
```

## Key Observations
- Image pulled from Docker Hub (cache miss on first run)
- Container ran as PID 1, exited with code 0 (clean)
- Auto-generated name: suspicious_jepsen
- Image digest: sha256:0e760fdfbc48... (content-addressable)

## 2026 Notes
- Use `docker container ls` not `docker ps` (management command syntax)
- Use `docker image ls` not `docker images`
- hello-world image unchanged since 2019 — stable reference image
