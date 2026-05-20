# Exercise 3.03 — Inspecting Image History and Layers

## Commands
```bash
docker image history my-first-image:1.0
docker image history php-welcome:1.0
docker image inspect my-first-image:1.0
docker image ls
```

## Key Observations

### my-first-image:1.0 layers
- ubuntu base: 87.7MB
- RUN apt-get install curl: 85MB (biggest layer)
- CMD, LABEL: 0B (metadata only)
- Total layers in RootFS: 2

### php-welcome:1.0 layers
- ubuntu base: 87.7MB
- RUN apt install apache2+php: 225MB (biggest layer!)
- COPY welcome.php: 20.5kB
- ENV, EXPOSE, ENTRYPOINT: 0B

### Image inspect revealed
- Architecture: amd64, OS: linux
- RepoTags: both my-first-image:1.0 and my-first-image:latest same ID
- Only 2 actual layers in RootFS despite 8 history entries

### nginx:1.27 tag and digest = same IMAGE ID
- digest pull and tag pull = same image on disk
- No duplicate storage

## 2026 Optimization Notes
- php-welcome 225MB RUN layer is too large
- Use official php:8.3-apache image instead of ubuntu base — saves ~200MB
- Zero-byte layers (CMD, LABEL, ENV, EXPOSE) don't add disk cost
- Fewer RUN commands = fewer layers = smaller image
