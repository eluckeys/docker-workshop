# Exercise 2.04 — WORKDIR, COPY and ADD Directives

## Dockerfile
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 -y
WORKDIR /var/www/html
COPY index.html .
CMD ["ls"]
```

## Commands
```bash
docker build -t workdir-copy-add:1.0 .
docker container run workdir-copy-add:1.0
```

## Key Observations
- WORKDIR sets working directory inside container — like cd but permanent
- COPY copies files from host to container — simple and predictable
- CMD ["ls"] ran in /var/www/html and showed index.html — WORKDIR + COPY proven
- ADD has extra powers: URL download + tar extraction — use COPY otherwise

## 2026 Notes
- Always use COPY over ADD unless you need URL download or tar extraction
- COPY is explicit and safer — ADD can have unexpected behavior
- For URL downloads use: RUN curl -o file.png https://... (more cacheable)
