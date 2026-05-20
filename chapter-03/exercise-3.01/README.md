# Exercise 3.01 — Pulling Images and Understanding Layers

## Commands
```bash
docker pull nginx:1.27
docker pull nginx:1.26
docker image ls
docker image history nginx:1.27
docker image history nginx:1.26
docker image inspect nginx:1.27 | grep -A 5 "Layers"
docker image inspect nginx:1.26 | grep -A 5 "Layers"
```

## Key Observations
- nginx:1.26 and nginx:1.27 share ZERO layers — completely different Debian snapshots
- No "Already exists" during nginx:1.26 pull — confirmed by inspect
- Total disk usage: ~564MB (282MB each, no deduplication)
- <missing> in history = BuildKit image from Docker Hub, intermediate metadata not stored locally
- Only final image ID visible locally, intermediate layer IDs missing

## Layer Digests — No Match
nginx:1.27: 7fb72a7d, 626ab8a5, 892e805f, 3e961627, 4197a611
nginx:1.26: ea680fbf, cf141407, c9829892, 67aafe50, 609897c8

## 2026 Notes
- Use digest pinning in production for guaranteed reproducibility
  docker pull nginx@sha256:6784fb0834aa...
- Tag :latest or even :1.27 can change — digest never changes
- Layer sharing only happens when exact same layer digest exists locally
