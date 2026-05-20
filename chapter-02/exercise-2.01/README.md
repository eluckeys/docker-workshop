# Exercise 2.01 — Creating Our First Dockerfile

## Dockerfile
```dockerfile
FROM ubuntu:22.04
LABEL maintainer="Saurabh S"
RUN apt-get update && apt-get install -y curl
CMD ["echo", "Hello from my first Docker image!"]
```

## Commands
```bash
docker build -t my-first-image:1.0 .
docker run my-first-image:1.0
docker run my-first-image:1.0 echo "I overrode the default CMD"
docker run my-first-image:1.0 curl --version
```

## Key Observations
- dot (.) in docker build = build context is current directory
- FROM = base layer
- RUN = executes at BUILD time, baked into image layer
- CMD = executes at RUN time, overridable
- LABEL = metadata, like a sticker on the image

## 2026 Notes
- Always pin base image: ubuntu:22.04 not ubuntu:latest
- Use JSON array format for CMD: ["cmd", "arg"]
- docker buildx is default build engine in Docker 29.x
