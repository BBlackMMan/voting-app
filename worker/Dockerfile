# Dockerfile pour le module "worker"

# Utiliser l'image officielle .NET SDK 7
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier tous les fichiers du projet avant de restaurer
COPY . .

# Supprimer les fichiers de cache NuGet potentiellement corrompus
RUN rm -rf obj/ project.assets.json

# Ajouter manuellement le package Newtonsoft.Json avant de restaurer
RUN dotnet add package Newtonsoft.Json --version 13.0.1

# Restaurer les dépendances et vérifier qu'elles sont bien installées
RUN dotnet nuget locals all --clear && dotnet restore

# Vérifier que les packages sont bien installés
RUN dotnet list package

# Vérifier la présence des fichiers avant compilation
RUN ls -l /app

# Compiler l'application en mode Release
RUN dotnet build -c Release --no-restore

# Publier l'application
RUN dotnet publish -c Release --self-contained false --no-restore -o /publish

# Utiliser une image plus légère pour exécuter l'application
FROM mcr.microsoft.com/dotnet/runtime:7.0

# Définir le répertoire de travail
WORKDIR /app

# Copier l'application publiée depuis l'étape précédente
COPY --from=build /publish .

# Lancer l'application
CMD ["dotnet", "Worker.dll"]
