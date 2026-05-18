# Exercise 1.03 — Attaching to an Ubuntu Container

## Commands
docker run -it ubuntu /bin/bash

## Key Observations
- ubuntu:latest pulled Ubuntu 26.04 (Resolute Raccoon) — newer than host (22.04)
- Container runs as root by default — security concern
- Hostname = container ID (UTS namespace isolation)
- /bin/bash was PID 1 — exit kills the container
- Full isolated filesystem via mount namespace

## 2026 Notes
- Never use ubuntu:latest in production — pin to specific version e.g. ubuntu:22.04
- Containers run as root by default — always add USER directive in Dockerfile
- -it flags required for interactive shell (i=STDIN open, t=pseudo-TTY)
