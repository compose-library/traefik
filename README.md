# Docker Compose for Traefik

## Config
- To generate a random password for Traefik admin use `echo $(htpasswd -nb admin $(openssl rand -base64 12)) | sed -e s/\\$/\\$\\$/g` and add the password to .env

## Usage
- To use Traefik's routing in your other Docker Compose projects, use the networks and label blocks like here:

```yaml
version: "3.5"

services:
  server:
    image: nginx:alpine
    networks:
      - traefik
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.sample.rule=Host(`${DOMAIN}`)"
      - "traefik.http.routers.sample.entrypoints=websecure,web"
      - "traefik.http.routers.sample.service=service-sample"
      - "traefik.docker.network=gateway"
      - "traefik.http.routers.sample.tls.certresolver=letsencrypt"
      - "traefik.http.services.service-sample.loadbalancer.server.port=80"

networks:
  traefik_default:
    external:
      name: traefik
```
