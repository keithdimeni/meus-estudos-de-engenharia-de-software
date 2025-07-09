# Docker - Guia Prático

## Instalação

### Ubuntu/Debian
```bash
# Atualizar pacotes
sudo apt-get update

# Instalar dependências
sudo apt-get install ca-certificates curl gnupg lsb-release

# Adicionar chave GPG oficial
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Adicionar repositório
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Instalar Docker Engine
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Adicionar usuário ao grupo docker
sudo usermod -aG docker $USER
```

### macOS
```bash
# Instalar Docker Desktop
brew install --cask docker
```

### Windows
- Baixar Docker Desktop do site oficial
- Habilitar WSL2 se necessário

## Comandos Essenciais

### Ciclo de Vida do Container
```bash
# Criar e executar
docker run -it ubuntu:22.04 /bin/bash
docker run -d -p 8080:80 --name webserver nginx

# Gerenciar containers
docker start webserver
docker stop webserver
docker restart webserver
docker pause webserver
docker unpause webserver

# Remover
docker rm webserver
docker rm -f webserver  # força remoção
```

### Trabalhando com Imagens
```bash
# Buscar imagem no Docker Hub
docker search redis

# Baixar imagem
docker pull redis:7-alpine

# Listar imagens locais
docker images
docker images -q  # apenas IDs

# Construir imagem
docker build -t meuapp:v1 .
docker build -f Dockerfile.prod -t meuapp:prod .

# Tag e push
docker tag meuapp:v1 meuuser/meuapp:v1
docker push meuuser/meuapp:v1
```

### Debugging e Monitoramento
```bash
# Logs
docker logs webserver
docker logs -f webserver  # follow
docker logs --tail 50 webserver

# Processos rodando
docker top webserver

# Estatísticas em tempo real
docker stats
docker stats webserver

# Inspecionar
docker inspect webserver
docker inspect webserver | jq '.[0].NetworkSettings.IPAddress'

# Executar comandos
docker exec webserver ls -la
docker exec -it webserver /bin/bash
```

## Dockerfile - Exemplos Práticos

### Node.js Application
```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

# Runtime stage
FROM node:18-alpine
WORKDIR /app
RUN addgroup -g 1001 -S nodejs && adduser -S nodejs -u 1001
COPY --from=builder /app/node_modules ./node_modules
COPY --chown=nodejs:nodejs . .
USER nodejs
EXPOSE 3000
CMD ["node", "server.js"]
```

### Python Application
```dockerfile
FROM python:3.11-slim

# Evitar arquivos .pyc e buffering
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Instalar dependências
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar aplicação
COPY . .

# Usuário não-root
RUN useradd -m -u 1001 appuser && chown -R appuser /app
USER appuser

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "app:app"]
```

## Docker Compose

### Exemplo: Stack Web Completa
```yaml
version: '3.8'

services:
  web:
    build: 
      context: .
      dockerfile: Dockerfile
    container_name: myapp-web
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:pass@db:5432/myapp
      - REDIS_URL=redis://cache:6379
    ports:
      - "3000:3000"
    depends_on:
      - db
      - cache
    restart: unless-stopped
    networks:
      - app-network

  db:
    image: postgres:15-alpine
    container_name: myapp-db
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: myapp
    volumes:
      - postgres-data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - app-network

  cache:
    image: redis:7-alpine
    container_name: myapp-cache
    command: redis-server --appendonly yes
    volumes:
      - redis-data:/data
    networks:
      - app-network

  nginx:
    image: nginx:alpine
    container_name: myapp-nginx
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - web
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  postgres-data:
  redis-data:
```

### Comandos Docker Compose
```bash
# Subir stack
docker-compose up -d

# Ver logs
docker-compose logs -f web

# Executar comando em serviço
docker-compose exec db psql -U user myapp

# Parar e remover
docker-compose down
docker-compose down -v  # remove volumes também
```

## Volumes e Persistência

### Tipos de Montagem
```bash
# Volume nomeado (recomendado para produção)
docker run -v mydata:/data postgres

# Bind mount (desenvolvimento)
docker run -v $(pwd)/src:/app/src node-app

# tmpfs mount (dados temporários em RAM)
docker run --tmpfs /tmp postgres
```

### Gerenciar Volumes
```bash
# Criar volume
docker volume create mydata

# Listar volumes
docker volume ls

# Inspecionar
docker volume inspect mydata

# Remover
docker volume rm mydata
docker volume prune  # remove não utilizados
```

## Networking

### Tipos de Network
```bash
# Bridge (padrão)
docker run --network bridge nginx

# Host (compartilha network do host)
docker run --network host nginx

# None (sem network)
docker run --network none nginx

# Custom network
docker network create mynet
docker run --network mynet --name web nginx
docker run --network mynet alpine ping web
```

### Comandos de Network
```bash
# Listar networks
docker network ls

# Inspecionar
docker network inspect bridge

# Conectar container
docker network connect mynet container1

# Desconectar
docker network disconnect mynet container1
```

## Otimização e Segurança

### Multi-stage Build
```dockerfile
# Exemplo completo com cache de dependências
FROM golang:1.21-alpine AS builder
WORKDIR /app
# Cache de dependências
COPY go.mod go.sum ./
RUN go mod download
# Build
COPY . .
RUN CGO_ENABLED=0 go build -o main .

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/main .
CMD ["./main"]
```

### Scan de Segurança
```bash
# Docker Scout (built-in)
docker scout quickview myapp:latest
docker scout cves myapp:latest

# Trivy
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
  aquasec/trivy image myapp:latest
```

## Troubleshooting

### Problemas Comuns

#### Container não inicia
```bash
# Ver últimos eventos
docker events --since '5m'

# Debug com shell
docker run -it --entrypoint /bin/sh myimage
```

#### Falta de espaço
```bash
# Ver uso de disco
docker system df

# Limpeza completa
docker system prune -a --volumes

# Limpar build cache
docker builder prune
```

#### Problemas de rede
```bash
# Testar conectividade
docker run --rm alpine ping google.com

# Ver configuração de rede
docker network inspect bridge
```

## Scripts Úteis

### Backup de volumes
```bash
#!/bin/bash
# backup-volume.sh
VOLUME_NAME=$1
BACKUP_PATH=$2

docker run --rm \
  -v ${VOLUME_NAME}:/source \
  -v ${BACKUP_PATH}:/backup \
  alpine tar czf /backup/${VOLUME_NAME}-$(date +%Y%m%d).tar.gz -C /source .
```

### Health check customizado
```bash
#!/bin/bash
# healthcheck.sh
curl -f http://localhost:8080/health || exit 1
```

## Integração com CI/CD

### GitHub Actions
```yaml
- name: Build and push Docker image
  uses: docker/build-push-action@v4
  with:
    context: .
    push: true
    tags: |
      user/app:latest
      user/app:${{ github.sha }}
```

### GitLab CI
```yaml
docker-build:
  image: docker:latest
  stage: build
  services:
    - docker:dind
  script:
    - docker build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA .
    - docker push $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
```

---
*Última atualização: [Data]*
*Docker version: 24.x*