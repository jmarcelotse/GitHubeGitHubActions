1. Projeto no Github
2. Actions - Set up workflow yourself

Passo para subir as imagens
    1. Autenticar no Docker Hub (Docker Login)
    2. Executar o comando docker build
    3. Executar o comando docker push

Secrets

          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
No repositorio criar as secrets
    Settings - Security - Secrets and Variables - Actions - New repository secret

name: CI-CD
on:
  push:
    branches: ["main"]
  workflow_dispatch:
jobs:
  CI:
    runs-on: ubuntu-latest
    steps:
    - name: Obtendo o código
      uses: actions/checkout@v4
    - name: Autenticação no Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}
    - name: Build da Imagem Docker
      uses: docker/build-push-action@v5
      with:
        context: ./src
        file: ./src/Dockerfile
        push: true
        tags: |
          jmarcelotse/primeira-pipeline:v${{ github.run_number }}
          jmarcelotse/primeira-pipeline:latest

    docker container run -d -p 8080:5000 jmarcelotse/primeira-pipeline:v4

    CD
    1 Configuracao do kubeconfig
    2 kubectl

  ###########

  name: CI-CD
on:
  push:
    branches: ["main"]
  workflow_dispatch:

jobs:
  CI:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout do código
      uses: actions/checkout@v4

    - name: Autenticação no Docker Hub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Build e push da imagem Docker
      uses: docker/build-push-action@v5
      with:
        context: ./src
        file: ./src/Dockerfile
        push: true
        tags: |
          jmarcelotse/primeira-pipeline:v${{ github.run_number }}
          jmarcelotse/primeira-pipeline:latest

  CD:
    runs-on: ubuntu-latest
    needs: [CI]
    steps:
    - name: Checkout do código
      uses: actions/checkout@v4

    - name: Configuração do contexto Kubernetes
      uses: azure/k8s-set-context@v4
      with:
        method: kubeconfig
        kubeconfig: ${{ secrets.K8S_CONFIG_AZ }}

    - name: Verificar contexto atual do Kubernetes (depuração)
      run: kubectl config current-context

    - name: Listar nós do Kubernetes (depuração)
      run: kubectl get nodes

    - name: Implantação no Kubernetes
      uses: Azure/k8s-deploy@v5
      with:
        manifests: ./k8s/deployment.yaml
        images: jmarcelotse/primeira-pipeline:v${{ github.run_number }}
