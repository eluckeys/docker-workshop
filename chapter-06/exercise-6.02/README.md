# Exercise 6.02 — Working with Docker DNS

## Commands
```bash
# Legacy --link method
docker run -itd --name containerlink1 alpine:latest
docker run -itd --name containerlink2 --link containerlink1 alpine:latest
docker exec -it containerlink2 /bin/sh
# ping containerlink1 → SUCCESS (one-way)
# cat /etc/hosts → hardcoded IP entry

docker exec -it containerlink1 /bin/sh
# ping containerlink2 → FAIL (--link is one-way)

# Custom bridge DNS method
docker network create dnsnet --subnet 192.168.54.0/24 --gateway 192.168.54.1
docker run -itd --network dnsnet --name aplinedns1 alpine:latest
docker run -itd --network dnsnet --name aplinedns2 alpine:latest
docker exec -it aplinedns1 /bin/sh
# ping aplinedns2 → SUCCESS
docker exec -it aplinedns2 /bin/sh
# ping aplinedns1 → SUCCESS (bidirectional!)
```

## Key Observations
- alpine:test tag not found — book outdated, used alpine:latest (v3.23.4)
- --link = one-way DNS via /etc/hosts injection — deprecated
- Custom bridge = bidirectional DNS via Docker embedded DNS server
- containerlink1 could NOT ping containerlink2 — --link limitation proven
- aplinedns1 and aplinedns2 pinged each other by name — custom bridge DNS proven
- New bridge interface br-ccab9557b3fe appeared in ip a after network create

## Network Comparison
| Feature | --link (legacy) | Custom Bridge |
|---|---|---|
| DNS direction | One-way | Bidirectional |
| Implementation | /etc/hosts | Docker DNS server |
| 2026 status | Deprecated | Standard |

## 2026 Notes
- Never use --link in new projects — deprecated since Docker 1.9
- Always create custom bridge networks for container communication
- Docker embedded DNS runs on 127.0.0.11 inside containers
- Each docker network create = new Linux bridge interface on host
