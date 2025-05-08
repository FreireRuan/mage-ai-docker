# ⚙️ Mage.ai em EC2 com Docker

Este repositório documenta o processo completo de instalação e exposição do Mage.ai em uma instância EC2 Ubuntu utilizando Docker.

---

## 🎯 Objetivo

Subir uma instância Mage.ai em uma EC2 limpa, de forma conteinerizada, com acesso externo via IP público e porta 6789.

---

## 📦 Pré-requisitos

- Instância EC2
- Acesso por usuário/senha ou chave
- Security Group com porta **6789** liberada

---

## 🐳 Instalação do Docker

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git unzip gnupg

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

exit  # reconectar
```

### 📂 Criar estutura do projeto

```bash
mkdir ~/mage_project && cd ~/mage_project
nano docker-compose.yml
```

### 📔 Conteúdo do docker-compose.yml

```yaml
version: '3.8'

services:
  mage:
    image: mageai/mageai:latest
    container_name: mage
    command: mage start mage_project
    ports:
      - 6789:6789
    volumes:
      - ./mage_project:/home/src
    environment:
      - USER_CODE_PATH=/home/src
```
### 🛜 Utilização Docker
``` git bash
ssh <USUARIO>@<IP_PÚBLICO_DA_EC2>
docker compose up -d
http://<IP_PÚBLICO_DA_EC2>:6789
```

## 🛠️ Comandos úteis
``` git bash
docker compose up -d	  ## Sobe o Mage em segundo plano
docker compose down	      ## Para e remove o container
docker logs mage	      ## Ver logs do Mage
docker ps	              ## Ver containers rodando
curl ifconfig.me	      ## Descobrir IP público da EC2
```

Feito com café ☕, Python 🐍 e umas ideias insanas 🛠️ por **Ruan Freire**  
🔗 [LinkedIn](https://www.linkedin.com/in/ruanfreire) • [GitHub](https://github.com/FreireRuan)
