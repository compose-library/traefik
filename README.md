# Docker Compose for Traefik

## Config
- To generate a random password for Traefik admin use `echo $(htpasswd -nb admin $(openssl rand -base64 12)) | sed -e s/\\$/\\$\\$/g` and add the password to .env