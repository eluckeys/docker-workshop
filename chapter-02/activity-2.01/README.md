# Activity 2.01 — Running a PHP Application on Docker Container

## Dockerfile
```dockerfile
FROM ubuntu:22.04
LABEL maintainer=SS
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y apache2 php libapache2-mod-php
COPY welcome.php /var/www/html/
EXPOSE 80
ENTRYPOINT ["apache2ctl", "-D", "FOREGROUND"]
```

## Commands
```bash
docker build -t php-welcome:1.0 .
docker container run -d -p 80:80 --name php-welcome php-welcome:1.0
curl http://localhost/welcome.php
```

## Output
Good Morning (time-based greeting)

## Mistakes Made and Fixed
1. COPY /var/www/html . — wrong, host path does not exist
   Fixed: COPY welcome.php /var/www/html/
2. apache2chtl — typo in ENTRYPOINT
   Fixed: apache2ctl
3. $houeOfDay — typo in PHP variable
   Fixed: $hourOfDay
4. Build hung on timezone prompt
   Fixed: Added ENV DEBIAN_FRONTEND=noninteractive
5. Port 80 already in use by onbuild-child-container
   Fixed: Stopped onbuild container first

## Key Observations
- DEBIAN_FRONTEND=noninteractive mandatory for Ubuntu-based images
- Port conflicts must be resolved before running new container on same port
- curl returned Apache 404 first — proved Apache was running but file missing

## 2026 Notes
- For production PHP apps use official php:8.x-apache image, not ubuntu base
- Multi-stage builds keep final image smaller
- Never run Apache as root in production
