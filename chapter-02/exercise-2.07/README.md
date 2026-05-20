# Exercise 2.07 — EXPOSE and HEALTHCHECK Directives

## Dockerfile
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 curl -y
HEALTHCHECK CMD curl -f http://localhost/ || exit 1
EXPOSE 80
ENTRYPOINT ["apache2ctl", "-D", "FOREGROUND"]
```

## Commands
```bash
docker build -t expose-healthcheck:1.0 .
docker container run -p 80:80 --name expose-healthcheck-container -d expose-healthcheck:1.0
docker container ls
docker container stop expose-healthcheck-container
docker container rm expose-healthcheck-container
```

## Key Observations
- EXPOSE = documentation only, does NOT bind port
- Actual port binding = docker run -p 80:80 (host:container)
- HEALTHCHECK: status showed "health: starting" then "healthy"
- ENTRYPOINT vs CMD: ENTRYPOINT not easily overridden, container dedicated to one app
- First use of ENTRYPOINT — apache2ctl is always PID 1

## 2026 Notes
- HEALTHCHECK is critical for Kubernetes readiness/liveness probes
- In K8s, unhealthy containers are restarted automatically
- Use --health-interval, --health-retries flags for fine tuning
