# Variáveis de Ambiente

As variáveis de ambiente no GitHub Actions são usadas para armazenar informações sensíveis, configurações personalizadas ou dados que são compartilhados entre diferentes passos ou jobs em um workflow. Elas podem ser definidas no nível do workflow, no nível do job ou globalmente no repositório. Vamos explorar como usar variáveis de ambiente com alguns exemplos:

# Definindo Variáveis de Ambiente no Nível do Workflow

Você pode definir variáveis de ambiente no nível do workflow usando a chave **env**. Essas variáveis são acessíveis em todos os jobs e steps dentro desse workflow.

**Exemplo**:

    yaml

    name: Example Workflow

    on: [push]

    env:
    ENVIRONMENT: production
    DATABASE_URL: ${{ secrets.DATABASE_URL }}

    jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Print environment variables
            run: |
            echo "Environment: $ENVIRONMENT"
            echo "Database URL: $DATABASE_URL"

Neste exemplo, definimos duas variáveis de ambiente, **ENVIRONMENT** e **DATABASE_URL**, que são usadas em um job para imprimir informações.

# Passando Variáveis de Ambiente para um Job Específico

Você também pode definir variáveis de ambiente diretamente em um job usando a chave **env**.

Exemplo:

yaml

    jobs:
    test:
        runs-on: ubuntu-latest
        env:
        NODE_ENV: test
        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Run tests
            run: npm test

Neste exemplo, definimos a variável **NODE_ENV** apenas para o job **test**, especificando-a na seção **env** do job.

# Usando Variáveis de Ambiente Secretas

Você pode armazenar variáveis de ambiente sensíveis, como chaves de API ou tokens de acesso, como segredos no GitHub e acessá-las nos workflows como variáveis de ambiente.

**Exemplo**:

    yaml

    name: Secret Example Workflow

    on: [push]

    env:
    API_KEY: ${{ secrets.API_KEY }}

    jobs:
    deploy:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Deploy to production
            run: |
            echo "Deploying with API key: $API_KEY"
            # Comandos de implantação usando a chave de API

Neste exemplo, acessamos a variável **API_KEY** definida como um segredo do GitHub no workflow para realizar uma implantação.

# Usando Variáveis de Ambiente Globalmente no Repositório

Você também pode definir variáveis de ambiente globalmente no repositório, que estarão disponíveis para todos os workflows e jobs.

Exemplo:

    yaml

    # Em .github/workflows/.env
    ENVIRONMENT=production
    DATABASE_URL=${{ secrets.DATABASE_URL }}

Estas variáveis estarão disponíveis em todos os workflows do repositório.

#Conclusão

As variáveis de ambiente são uma parte importante do GitHub Actions, permitindo a passagem de informações entre os diferentes passos e jobs de um workflow. Ao usar variáveis de ambiente, você pode manter suas configurações flexíveis, proteger informações sensíveis e tornar seus workflows mais dinâmicos e reutilizáveis.

######################

https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables

name: Usando variaveis de ambiente

on:
  workflow_dispatch:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
env:
  ENV_WORKFLOW: "Valor WORKFLOW"

jobs:
  teste-env:
    runs-on: ubuntu-latest
    env:
      ENV_JOB: "Valor JOB teste-env"

    steps:
      - name: Exexução
        env:
          ENV_ACTION: "Valor ACTION - Execução"
        run: |
          echo "$ENV_WORKFLOW"
          echo "$ENV_JOB"
          echo "$ENV_ACTION"

      - name: Exexução 2
        env:
          ENV_ACTION2: "Valor ACTION - Segunda Execução"
        run: |
          echo "$ENV_WORKFLOW"
          echo "$ENV_JOB"
          echo "$ENV_ACTION"
          echo "$ENV_ACTION2"

  teste-env2:
    runs-on: ubuntu-latest
    needs: [teste-env]
    env:
      ENV_JOB2: "Valor JOB Segundo teste-env"

    steps:
      - name: Exexução
        run: |
          echo "$ENV_WORKFLOW"
          echo "$ENV_JOB"
          echo "$ENV_JOB2"