# noVNC container deployment

noVNC docker deployment files for:

- docker-compose

- docker-swarm

## Requirements

- docker

- docker-swarm or docker-compose plugin

## Installation

```bash
sudo apt-get update
sudo apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
mkdir -p ~/.gnupg
chmod 700 ~/.gnupg
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
"deb [arch=$(dpkg --print-architecture) \
signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install -y \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    docker-compose-plugin
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

# Deploy

### Common

```bash
git clone https://github.com/RobotnikAutomation/novnc_container_deploy.git
cd novnc_container_deploy.git
checkout <TAG OR BRANCH>
```

### Registry login

**Note:** You will need credentials files to login into the registry

```bash
cat <CREDENTIALS_JSON_FILE> | \
docker login -u _json_key --password-stdin https://europe-west1-docker.pkg.dev
```

### Docker Compose

```bash
docker compose up -d
```

### Docker Swarm

```bash
docker swarm init
docker stack deploy --with-registry-auth --prune -c docker-compose.yaml  novnc
```
