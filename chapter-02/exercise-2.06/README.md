# Exercise 2.06 — VOLUME Directive

## Dockerfile
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 -y
VOLUME ["/var/log/apache2"]
CMD ["bash"]
```

## Commands
```bash
docker build -t volume-demo:1.0 .
docker container run -it --name volume-container volume-demo:1.0
# Inside container:
cd /var/log/apache2 && ls -l
exit
docker container inspect volume-container | grep Destination
docker volume ls
```

## Key Observations
- VOLUME creates a mount point that persists outside the container
- /var/log/apache2 mapped to /var/lib/docker/volumes/... on host
- Container deleted = volume still exists
- docker volume ls showed 3 volumes on disk

## 2026 Notes
- Named volumes preferred over anonymous: docker run -v mydata:/var/log/apache2
- Anonymous volumes (random hash names) are hard to manage at scale
- In production use: docker volume create, then mount with -v
