# Exercise 1.03 — Attaching to an Ubuntu Container

## Commands
docker run -itd --name attach-example1 ubuntu:latest
docker attach attach-example1
docker start <stopped-container>

## Key Observations
- -itd = interactive + TTY + detached (shell waiting in background)
- exit kills container — bash is PID 1
- Ctrl+P+Q detaches without stopping — container stays running
- Cannot attach to stopped container — must start first

## 2026 Notes
- ubuntu:latest = Ubuntu 26.04 in May 2026 — pin versions in production
- Use --name always — random names are unmanageable at scale
