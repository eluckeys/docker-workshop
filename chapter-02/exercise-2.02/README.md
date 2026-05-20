# Exercise 2.02 — Building and Tagging a Docker Image

## Commands
```bash
docker image tag my-first-image:1.0 my-first-image:latest
docker image tag my-first-image:1.0 my-first-image:stable
docker image ls
docker image rm my-first-image:stable
docker image ls
```

## Key Observations
- Tag = pointer to IMAGE ID, not a copy
- my-first-image:1.0 and my-first-image:latest had same IMAGE ID — proven
- Removing a tag does not delete the image if other tags still point to it
- Image only deleted when NO tags point to it

## 2026 Notes
- Always use semantic versioning: image:1.0, image:1.0.1
- Never rely on :latest in production — unpredictable
- Tag format for Docker Hub: username/image-name:tag
