# 1 - Configuration Jenkins pour build/push Docker

- Name: Integration-Delivery-Pipeline-Frontend
- Type: Pipeline script from SCM
- Repository URL: https://github.com/danphannguyen/efrei_frontend_crisisview.git
- Branch specifier: */main
- Script path: Jenkinsfile.cicd
- Add Parameter → "String Parameter".
  - `APP_NAME` - nom de l'application, ici `efrei-frontend-crisiview` (utilisé pour Sonar et Docker)
  - `API_URL` - URL de l'API Backend pour ce déploiement (exemple : `http://192.168.64.11:3001`)
  - `DOCKERHUB_NAMESPACE`: votre nom d'utilisateur ou organisation Docker Hub (ex: `dvnpn`)
  - `DOCKERHUB_REPO_NAME`: nom du repository Docker Hub pour l'image web (ex: `efrei-frontend-crisiview`). **Obligatoire** — le pipeline échouera si non défini.

⚠️ Avant de lancer la pipeline il faut impérativement créer les repository sur Dockerhub ⚠️

# 2 - Configuration Jenkins pour Deploy

- Name: Deploy-Pipeline-Frontend
- Type: Pipeline script from SCM
- Repository URL: https://github.com/danphannguyen/efrei_frontend_crisisview.git
- Branch specifier: */main
- Script path: Jenkinsfile.deploy
- Add Parameter → "String Parameter".
  - `APP_NAME` - nom de l'application, ici `efrei-frontend-crisiview` (utilisé pour Docker)
  - `DEPLOY_HOST`: l'ip de votre machine de déploiement
  - `DEPLOY_USER`: Utilisateur SSH pour le déploiement
  **Obligatoire** — le pipeline échouera si non défini.