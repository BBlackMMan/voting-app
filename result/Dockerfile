# Dockerfile pour le module "result"

# Utiliser une image Node.js 18
FROM node:18

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier les fichiers package.json et package-lock.json
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers du projet
COPY . .

# Exposer le port utilisé par l'application
EXPOSE 8888

# Lancer l'application
CMD ["npm", "start"]
