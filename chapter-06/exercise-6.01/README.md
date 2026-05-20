# Exercise 6.01 — Hands-On with Docker Networking

## Commands
```bash
docker network ls
ip a
docker run -d --name webserver1 nginx:latest
docker inspect webserver1
ip a
curl 172.17.0.2
docker run -d -p 8080:80 --name webserver2 nginx:latest
curl localhost:8080
docker exec -it webserver1 /bin/bash
# Inside:
apt update && apt install -y inetutils-ping curl
ping 172.17.0.3
curl 172.17.0.3
exit
```

## Key Observations
- 3 default networks always present: bridge, host, none
- docker0 interface = virtual switch — DOWN when no containers, UP when container attached
- Container without -p = internal only (172.17.0.2) — host can reach but outside cannot
- Container with -p 8080:80 = port binding via iptables DNAT — accessible from outside
- vethfb2e6a5@if2 appeared after container start — virtual ethernet pair (veth)
- webserver1 IP: 172.17.0.2, webserver2 IP: 172.17.0.3
- ping 172.16.0.3 = 100% loss (wrong subnet), ping 172.17.0.3 = success
- Container to container communication works via bridge IP

## Network Layout
Host (192.168.122.11)
├── docker0 bridge (172.17.0.1)
│   ├── webserver1 (172.17.0.2) — no port binding
│   └── webserver2 (172.17.0.3) — port 8080:80
└── enp1s0 (192.168.122.11) — physical NIC

## 2026 Notes
- nginx:latest now uses debian:trixie-slim (Debian 13) — was buster in 2019
- NGINX version: 1.31.0 (book had older version)
- inetutils-ping needed instead of iputils-ping on Debian trixie
- veth pairs = how Docker connects container net namespace to bridge
- Port binding = iptables DNAT rule auto-created by Docker daemon
