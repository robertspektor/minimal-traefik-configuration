# Minimal Traefik Configuration

Hi! This is my minimal Traefik Configuration I want to share with you. You can use it for you local development as well on production server.

## Run local configuration

### 1. Create network
```
docker network create traefik-public
```

### 2. Adjust docker-compose.yml

```
- "traefik.http.routers.traefik.rule=Host(`traefik.example.com`)"
```

### 3. Start Traefik
```
docker compose up --build -d
```

## Run production configuration

### 1. First create network
```
docker network create traefik-public
```

### 2. Adjust docker-compose-prod.yml

#### Email for letsencrpyt
```
- "--certificatesresolvers.letsencryptresolver.acme.email=someone@example.com"
```

#### Host
```
- "traefik.http.routers.traefik.rule=Host(`traefik.example.com`)"
```

#### Generate Basic Authentication Header
```
- "traefik.http.middlewares.traefik-auth.basicauth.users=admin:$$apr1$$t3uj85rc$$I2M.hJC.0jo/eZyJQ35mK1"
```

Use: https://www.web2generators.com/apache-tools/htpasswd-generator

### 3. Start Traefik

```
docker compose -f docker-compose-prod.yml up --build -d
```
