# Simple deployment using SSH and Docker Compose

```yml
name: Deploy

on:
  push:
    branches:
      - master

jobs:
  test:
    name: Simple deployment using SSH and Docker Compose
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Deploy
        uses: einsenundnullen/deploy-action@master
        with:
          docker-compose-file: docker-compose-prod.yml
          docker-env-vars: ${{ secrets.PROD_ENV }}
          ssh-user: ci
          ssh-host: ${{ secrets.HOST }}
          ssh-private-key: ${{ secrets.PRIVATE_KEY }}
          working-directory: ./optional-working-directory
```
