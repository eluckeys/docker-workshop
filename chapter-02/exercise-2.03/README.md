# Exercise 2.03 — ENV and ARG Directives

## Dockerfile
```dockerfile
FROM ubuntu:22.04
ENV ENVIRONMENT=production
ENV APP_VERSION=1.0
ARG BUILD_DATE
LABEL build-date=$BUILD_DATE
RUN echo "Building version $APP_VERSION for $ENVIRONMENT"
CMD ["env"]
```

## Commands
```bash
docker build \
  --build-arg BUILD_DATE=$(date +%Y-%m-%d) \
  -t env-arg-demo:1.0 .
docker run env-arg-demo:1.0
```

## Key Observations
- ENV: available at BUILD time AND RUNTIME — baked into image permanently
- ARG: available at BUILD time ONLY — gone when container runs
- docker run output showed ENVIRONMENT=production and APP_VERSION=1.0
- BUILD_DATE was NOT in docker run output — ARG vs ENV proven

## 2026 Notes
- Never put secrets in ENV — visible in docker inspect and image layers
- Use Docker secrets or external secret managers (Vault, AWS SSM) for sensitive data
- ARG is safe for build-time config like dates, versions, git commits
