# Contextos

Contextos no GitHub Actions são coleções de variáveis ​​de ambiente, armazenadas em nível de organização ou repositório, que podem ser reutilizadas em vários workflows. Eles oferecem uma maneira conveniente de compartilhar informações comuns ou configurações entre diferentes workflows, jobs e steps, reduzindo a redundância e simplificando a manutenção.

# Características dos Contextos

- **Escopo**: Os contextos podem ser definidos em nível de organização ou repositório, permitindo que você compartilhe variáveis globalmente ou apenas dentro de um projeto específico.

- **Variáveis**: Eles consistem em variáveis de ambiente, que podem incluir segredos criptografados e valores comuns usados em seus workflows.

- **Segredos**: Os contextos podem conter segredos sensíveis, como tokens de acesso ou chaves de API, que são armazenados de forma segura e podem ser acessados ​​pelos workflows sem expor os valores diretamente.

# Usando Contextos

1. **Definindo Contextos**:
    - Você pode definir contextos no arquivo YAML do seu workflow ou configurá-los nas configurações do repositório no GitHub.

2. **Acessando Contextos**:
    - As variáveis definidas em um contexto podem ser acessadas nos workflows usando a sintaxe **${{ secrets.NOME_DO_SEGREDOS }}** ou **${{ env.NOME_DA_VARIAVEL }}**.

# Exemplo de Uso de Contextos
**Definindo um Contexto no Arquivo YAML do Workflow**:

    yaml
    jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Print environment variables
            run: |
            echo "API key: ${{ secrets.API_KEY }}"
            echo "Environment: ${{ env.ENVIRONMENT }}"

**Configurando um Contexto no GitHub**:

1. **Criar um Arquivo de Contexto**:
    - Crie um arquivo YAML com suas variáveis e segredos:

    yaml
    # Arquivo: my-context.yml
    name: my-context
    env:
        ENVIRONMENT: production
    secrets:
    API_KEY: ${{ secrets.MEU_SEGREDO }}

2. **Adicionar o Arquivo ao Repositório**:

    - Adicione este arquivo ao diretório **.github** do seu repositório.

3. **Referenciar o Contexto no Workflow**:

    - Use o contexto no seu workflow:

    yaml
    jobs:
    build:
        runs-on: ubuntu-latest
        env:
        ENVIRONMENT: ${{ secrets.MEU_SEGREDO }}
        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Print environment variables
            run: |
            echo "API key: ${{ secrets.API_KEY }}"
            echo "Environment: ${{ env.ENVIRONMENT }}"

# Benefícios dos Contextos

- **Reutilização**: Evita a duplicação de configurações, permitindo que você defina variáveis comuns uma vez e as reutilize em vários workflows.

- **Segurança**: Segredos são criptografados e armazenados de forma segura, permitindo que você gerencie e compartilhe informações sensíveis com segurança.

- **Facilidade de Manutenção**: Simplifica a manutenção e a atualização de variáveis, especialmente em grandes projetos com múltiplos workflows.

# Conclusão

Os contextos no GitHub Actions oferecem uma maneira conveniente e segura de compartilhar e reutilizar variáveis e segredos em seus workflows. Ao definir contextos em nível de organização ou repositório, você pode melhorar a organização, a segurança e a manutenção dos seus workflows, garantindo um desenvolvimento mais eficiente e confiável.

name: Como usar variavel de ambiente e contexto do GitHub Actions
on:
    push:
        branches: [main]
env:
  ENV_WORKFLOW: "Valor WORKFLOW"
jobs:
  contextos:
    runs-on: ubuntu-latest
    env:
        ENV_JOB: "Valor JOB CONTEXT"
    steps:
      - name: Contexto github
        env:
          GITHUB_CONTEXT: ${{ toJson(github) }}
        run: echo "$GITHUB_CONTEXT"
      - name: Contexto env
        env:
          ENV_CONTEXT: ${{ toJson(env) }}
        run: echo "$ENV_CONTEXT"
      - name: Contexto job
        env:
          JOB_CONTEXT: ${{ toJson(job) }}
        run: echo "$JOB_CONTEXT"
      - name: Contexto steps
        env:
          STEPS_CONTEXT: ${{ toJson(steps) }}
        run: echo "$STEPS_CONTEXT"
      - name: Contexto runner
        env:
          RUNNER_CONTEXT: ${{ toJson(runner) }}
        run: echo "$RUNNER_CONTEXT"


https://docs.github.com/pt/actions/learn-github-actions/contexts