# JellyPlex-Watched

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/26b47c5db63942f28f02f207f692dc85)](https://www.codacy.com/gh/luigi311/JellyPlex-Watched/dashboard?utm_source=github.com&utm_medium=referral&utm_content=luigi311/JellyPlex-Watched&utm_campaign=Badge_Grade)

Synchronisez l'état de visionnage entre Jellyfin, Plex et Emby localement.

## Description

Maintenez synchronisé l'historique de visionnage de tous vos utilisateurs entre les serveurs Jellyfin, Plex et Emby localement. Ce script utilise les noms de fichiers et les identifiants de fournisseurs (provider IDs) pour trouver le bon épisode/film. Ce n'est pas parfait, mais cela fonctionne dans la plupart des cas. Vous pouvez l'utiliser pour autant de serveurs que vous le souhaitez en saisissant plusieurs options dans la section Plex/Jellyfin du fichier .env, séparées par des virgules.

## Fonctionnalités

### Plex

- \[x] Correspondance via les noms de fichiers
- \[x] Correspondance via les identifiants de fournisseurs
- \[x] Mapper les noms d'utilisateurs
- \[x] Utiliser une seule connexion
- \[x] Synchronisation unidirectionnelle/multidirectionnelle
- \[x] Synchroniser l'état "vu"
- \[x] Synchroniser la progression "en cours"
- \[ ] Synchroniser les dates de visionnage

### Jellyfin

- \[x] Correspondance via les noms de fichiers
- \[x] Correspondance via les identifiants de fournisseurs
- \[x] Mapper les noms d'utilisateurs
- \[x] Utiliser une seule connexion
- \[x] Synchronisation unidirectionnelle/multidirectionnelle
- \[x] Synchroniser l'état "vu"
- \[x] Synchroniser la progression "en cours"
- \[x] Synchroniser les dates de visionnage

### Emby

- \[x] Correspondance via les noms de fichiers
- \[x] Correspondance via les identifiants de fournisseurs
- \[x] Mapper les noms d'utilisateurs
- \[x] Utiliser une seule connexion
- \[x] Synchronisation unidirectionnelle/multidirectionnelle
- \[x] Synchroniser l'état "vu"
- \[x] Synchroniser la progression "en cours"
- \[x] Synchroniser les dates de visionnage

## Configuration

La liste complète des options de configuration se trouve dans le fichier [.env.sample](.env.sample)

## Installation

### Directe (Baremetal)

- [Installer uv](https://docs.astral.sh/uv/getting-started/installation/)

- Créez un fichier .env similaire à .env.sample ; remplissez les baseurls et les tokens, **n'oubliez pas de décommenter tout ce que vous souhaitez utiliser** (par exemple, le mappage d'utilisateurs, le mappage de bibliothèques, les listes noires/blanches, etc.). Si vous souhaitez stocker votre fichier .env ailleurs ou sous un nom différent, vous pouvez utiliser la variable ENV_FILE pour spécifier l'emplacement.

- Exécuter

  ```bash
  uv run main.py
  ```

  ```bash
  ENV_FILE="Test.env" uv run main.py
  ```

### Docker

- Construire l'image Docker

  ```bash
  docker build -t jellyplex-watched .
  ```

- ou utiliser l'image pré-construite

  ```bash
  docker pull Turiko313/jellyplex-watched:latest
  ```

#### Avec des variables

- Exécuter

  ```bash
  docker run --rm -it -e PLEX_TOKEN='SuperSecretToken' Turiko313/jellyplex-watched:latest
  ```

#### Avec .env

- Créez un fichier .env similaire à .env.sample et définissez les variables pour qu'elles correspondent à votre configuration.

- Exécuter

  ```bash
   docker run --rm -it -v "$(pwd)/.env:/app/.env" Turiko313/jellyplex-watched:latest
  ```

## Dépannage/Problèmes

- Jellyfin

  - "Attempt to decode JSON with unexpected mimetype" : assurez-vous d'activer l'accès à distance ou d'ajouter votre sous-réseau Docker aux réseaux locaux dans les paramètres de Jellyfin.

- Configuration
  - N'utilisez pas de guillemets autour des variables dans Docker Compose.
  - Si vous n'utilisez pas les 3 serveurs pris en charge (Plex, Jellyfin et Emby) simultanément, assurez-vous de commenter l'URL et le token du serveur que vous n'utilisez pas.

## Contribuer

Je suis ouvert aux pull requests. Si vous en soumettez une, veuillez vous assurer de l'exécuter localement pendant un jour ou deux pour vérifier qu'elle fonctionne comme prévu et qu'elle est stable.

## Licence

Ce projet est actuellement sous la licence publique générale GNU v3.0.
