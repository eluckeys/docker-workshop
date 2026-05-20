# Exercise 3.02 — Pushing Image to Docker Hub

## Commands
```bash
docker login -u 1ucky
docker image tag php-welcome:1.0 1ucky/php-welcome:1.0
docker image push 1ucky/php-welcome:1.0
```

## Push Output
- 4 layers pushed — zero "Mounted from"
- ubuntu:22.04 local digest did not match Docker Hub library/ubuntu
- digest: sha256:1dc1f613...

## Key Observations
- Tag format for Docker Hub: username/image-name:tag
- docker login required before push
- Layer mounting saves bandwidth when base image digest matches Docker Hub
- All 4 layers pushed fresh in this case — no deduplication

## Docker Hub URL
https://hub.docker.com/r/1ucky/php-welcome

## 2026 Notes
- Docker Hub free account: 1 private repo, unlimited public repos
- Production: use private registry — AWS ECR, GitHub Container Registry (ghcr.io)
- Use access tokens instead of password for docker login (more secure)
  Settings → Security → New Access Token on hub.docker.com
