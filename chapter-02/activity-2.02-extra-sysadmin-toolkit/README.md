# Extra Activity — Sysadmin Toolkit Image

## Dockerfile
```dockerfile
FROM ubuntu:22.04
LABEL maintainer="Saurabh S"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    vim \
    && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY . .
CMD ["bash"]
```

## Commands
```bash
docker build -t sysadmin-toolkit:1.0 .
docker container run -it sysadmin-toolkit:1.0
# Inside:
curl --version
git --version
vim --version
exit
```

## Key Observations
- All tools installed in single RUN = single layer = smaller image
- rm -rf /var/lib/apt/lists/* in same RUN command removes apt cache
- If deleted in separate RUN, previous layer still has cache — size not reduced
- WORKDIR /app = landed directly in /app inside container
- All tools verified working inside container

## 2026 Notes
- rm -rf /var/lib/apt/lists/* must be in SAME RUN as apt-get install
- Separate RUN for cleanup = wasted space, layers are immutable
- This is a common Dockerfile optimization interview question
