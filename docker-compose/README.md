# Bitnami Kyecloak Docker Compose

# Docker Compose Installation

- https://hub.docker.com/r/bitnami/keycloak/
  
```bash
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
```

# Build

```bash
docker compose -p keycloak up -d --build
```

- DEBUG Check current configurations
```bash
/opt/bitnami/keycloak/bin/kc.sh show-config
```
