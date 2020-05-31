# Traefik proxy #

## How to build ##

```bash
docker-compose -f etc/docker/docker-compose.yml
```

## How to run ##

```yml
version: "3"
services:
  traefik_proxy:
    image: efc/traefik-proxy:1.0.0
    hostname: traefik-proxy
    ports:
      - "80:80"
      - "443:443"
    labels:
        # ##################################
        # Base service configuration
        - "traefik.enable=true"
        # ##################################
        # Service service configuration
        - "traefik.http.services.api@internal.loadbalancer.server.port=8080"
        # ##################################
        # Middlewares serviceconfiguration
        # ##################################
        # Insecure (http) router configuration
        - "traefik.http.routers.traefik_insecure.rule=PathPrefix(`/dashboard`)"
        - "traefik.http.routers.traefik_insecure.service=api@internal"
        - "traefik.http.routers.traefik_insecure.rule=Host(`dashboard.traefik.efc.io`)"
        - "traefik.http.routers.traefik_insecure.entrypoints=http"
        - "traefik.http.routers.traefik_insecure.middlewares=base_redirect_http_to_https@file"
        # ##################################
        # Secure (https) router configuration
        - "traefik.http.routers.traefik_secure_dashboard.rule=PathPrefix(`/dashboard`)"
        - "traefik.http.routers.traefik_secure_dashboard.service=api@internal"
        - "traefik.http.routers.traefik_secure_dashboard.rule=Host(`dashboard.traefik.efc.io`)"
        - "traefik.http.routers.traefik_secure_dashboard.tls=true"
        - "traefik.http.routers.traefik_secure_dashboard.entrypoints=https"
        - "traefik.http.routers.traefik_secure_dashboard.middlewares=dashboard_digest_auth@file"
    volumes:
      - "./letsencrypt:/letsencrypt"
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "../traefik/:/etc/traefik/dynamicConfiguration/"
```