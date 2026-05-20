FROM ubuntu:22.04
LABEL maintainer="SS"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y curl git wget vim && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY . .
CMD ["bash"]
