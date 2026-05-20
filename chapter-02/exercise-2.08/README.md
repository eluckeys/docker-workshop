# Exercise 2.08 — ONBUILD Directive

## Parent Dockerfile
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 -y
ONBUILD COPY *.html /var/www/html
EXPOSE 80
ENTRYPOINT ["apache2ctl", "-D", "FOREGROUND"]
```

## Child Dockerfile
```dockerfile
FROM onbuild-parent:1.0
```

## Commands
```bash
# Parent
docker build -t onbuild-parent:1.0 .
# Child
docker build -t onbuild-child:1.0 .
docker container run -p 80:80 --name onbuild-child-container -d onbuild-child:1.0
```

## Key Observations
- ONBUILD = deferred instruction, fires when someone uses this image as FROM
- Parent build: ONBUILD did nothing
- Child build: ONBUILD COPY triggered automatically — index.html copied
- Child Dockerfile had only 1 line — FROM onbuild-parent:1.0
- Child inherited all parent behavior + ONBUILD trigger

## 2026 Notes
- ONBUILD rarely used in modern Docker — multi-stage builds preferred
- Useful for base images shared across a team
- Can be confusing — always document ONBUILD in image README
