# Simple service deployment using GitHub Docker Registry, SSH and Docker Compose

```yml
name: Deploy

on:
  push:
    branches:
      - master

jobs:
  test:
    name: Clone, build, push and deploy
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Deploy
        uses: einsenundnullen/docker-compose-deploy-action@master
        with:
          docker-user: ${{ github.repository_owner }}
          docker-password: ${{ secrets.GITHUB_TOKEN }}
          docker-compose-file: docker-compose-prod.yml
          docker-env-vars: ${{ secrets.PROD_ENV }}
          ssh-user: ci
          ssh-host: ${{ secrets.HOST }}
          ssh-private-key: ${{ secrets.PRIVATE_KEY }}
          working-directory: ./optional-service-directory
```
