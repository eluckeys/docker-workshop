# Exercise 2.01 — Creating and Building a Dockerfile

## Dockerfile
FROM ubuntu:22.04
LABEL maintainer="Saurabh S"
RUN apt-get update && apt-get install -y curl
CMD ["echo", "Hello from my first Docker image!"]

## Commands
docker build -t my-first-image:1.0 .
docker run my-first-image:1.0
docker run my-first-image:1.0 echo "I overrode the default CMD"
docker run my-first-image:1.0 curl --version

## Key Observations
- dot (.) in docker build = build context is current directory
- FROM = base layer, RUN = build-time layer, CMD = runtime default
- CMD is overridable at runtime — pass command after image name
- RUN is baked in — curl always available regardless of CMD override
- Each Dockerfile instruction = one image layer

## 2026 Notes
- Always pin base image version — ubuntu:22.04 not ubuntu:latest
- Use JSON array format for CMD: ["cmd", "arg"] not CMD cmd arg
- docker buildx is default build engine in Docker 29.x
