# Chapter 2 — Getting Started with Dockerfiles

## Environment
- OS: Ubuntu 22.04 LTS (Jammy)
- Docker: 29.4.3
- Date: May 2026

## Exercises
- [x] Exercise 2.01 — Creating a Dockerfile
- [x] Exercise 2.02 — Building and Tagging a Docker Image
- [x] Exercise 2.03 — ENV and ARG Directives
- [x] Exercise 2.04 — WORKDIR, COPY and ADD Directives
- [x] Exercise 2.05 — USER Directive
- [x] Exercise 2.06 — VOLUME Directive
- [x] Exercise 2.07 — EXPOSE and HEALTHCHECK Directives
- [x] Exercise 2.08 — ONBUILD Directive
- [x] Activity 2.01 — PHP Application on Docker Container
- [x] Extra Activity — Sysadmin Toolkit Image

## Key Learnings
- Every Dockerfile instruction creates a new image layer
- RUN = build time, CMD = runtime, ENTRYPOINT = dedicated app
- ENV persists at runtime, ARG is build-time only
- Always use DEBIAN_FRONTEND=noninteractive for Ubuntu-based images
- USER directive — never run containers as root in production
- VOLUME — data persists even after container is deleted
- COPY preferred over ADD unless URL/tar extraction needed
- Clean apt cache in same RUN command — layers are immutable
