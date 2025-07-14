* ## Salut !!! Ceci est mon CheatSheet de Docker avec presque toute les notions que le Docteur Sitraka nous a appris jusqu'ici.

````markdown
# 🚢 Docker Cheatsheet

Petit guide express pour installer, lancer et orchestrer vos conteneurs Docker en toute simplicité.

---

## 📥 Installation

### Linux (Ubuntu)

```bash
sudo apt update
sudo apt install -y \
  apt-transport-https \
  ca-certificates \
  curl \
  software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  | sudo apt-key add -

sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable"

sudo apt update
sudo apt install -y docker-ce
sudo systemctl enable --now docker
````

### Windows & macOS

1. Télécharger **Docker Desktop** :
   [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Installer, puis redémarrer.

---

## ⚙️ Commandes de base

| Commande                             | Description                                  |
| ------------------------------------ | -------------------------------------------- |
| `docker --version`                   | Version de Docker                            |
| `docker pull <image>`                | Télécharger une image                        |
| `docker images`                      | Liste des images locales                     |
| `docker run -d --name <nom> <image>` | Lancer un conteneur en arrière‑plan          |
| `docker ps -a`                       | Afficher tous les conteneurs                 |
| `docker stop <container>`            | Arrêter un conteneur                         |
| `docker rm <container>`              | Supprimer un conteneur                       |
| `docker rmi <image>`                 | Supprimer une image                          |
| `docker exec -it <container> sh`     | Ouvrir un shell interactif dans le conteneur |

---

## 🐳 Dockerfile minimal

```dockerfile
# Base image
FROM node:18

# Créer et définir le dossier de travail
WORKDIR /app

# Copier et installer les dépendances
COPY package*.json ./
RUN npm install

# Copier le code source
COPY . .

# Exposer le port
EXPOSE 3000

# Lancer l’application
CMD ["npm", "start"]
```

> **Astuce** :
>
> ```bash
> docker build -t mon-app .
> ```

---

## 🧩 Docker Compose

```yaml
version: "3.8"

services:
  app:
    build: .
    container_name: mon_app
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:15
    container_name: ma_db
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

**Commandes clés**

```bash
docker-compose up -d      # Démarrer en arrière‑plan  
docker-compose down       # Arrêter et supprimer  
docker-compose logs -f    # Suivre les logs  
docker-compose build      # Reconstruire les images  
```

---

## 💡 Tips rapides

* **Sans sudo** :

  ```bash
  sudo usermod -aG docker $USER && newgrp docker
  ```
* **Nettoyage global** :

  ```bash
  docker system prune -a
  ```
* **Nettoyer volumes/images anciens** :

  ```bash
  docker volume prune
  docker image prune --filter "until=24h"
  ```

---

## 🔗 Liens utiles

* Docs officielles : [https://docs.docker.com/](https://docs.docker.com/)
* Docker Hub : [https://hub.docker.com/](https://hub.docker.com/)

---

> *« Conteneurisez vite, conteneurisez bien !»* 🚀🐳

```
```
