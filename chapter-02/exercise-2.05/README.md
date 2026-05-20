# Exercise 2.05 — USER Directive

## Dockerfile
```dockerfile
FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 -y
USER www-data
CMD ["whoami"]
```

## Commands
```bash
docker build -t user-demo:1.0 .
docker container run user-demo:1.0
```

## Key Observations
- Without USER directive: container runs as root (dangerous)
- With USER www-data: container runs as www-data — non-root
- Output: www-data — proven
- If attacker escapes container running as root = root on host

## 2026 Notes
- Always run containers as non-root in production
- Best practice: create dedicated user in Dockerfile
  RUN groupadd -r appuser && useradd -r -g appuser appuser
  USER appuser
- This is a STIG/CIS compliance requirement
