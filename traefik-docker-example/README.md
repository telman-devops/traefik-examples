# Traefik example for docker

### Features

- Dynamic Routing
- Load balancer
- Letsencrypt
- Web UI

> In this tutorial, we are managing docker host with [portainer](https://www.portainer.io/)

### Traefik Principles

- Entry points
- Frontends
- Backends
- Servers

## Let`s Start

1. **Create password for basicAuth**

Install apache utils
```
apt-get install apache2-utils
```
Generate password
```
htpasswd -nb admin somepass
```
Paste generate password to `./traefik-data/configurations/dynamic.yml`

2. **Create docker network**
```
docker network create proxy
```

3. **Change permission acme.json**
```
chmod 600 acme.json
```

4. **Run docker composer**
```
docker-compose up or docker-compose up -d
```

> [Site](https://dnschecker.org/) helps to dns check

