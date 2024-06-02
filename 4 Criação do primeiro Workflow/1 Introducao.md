# Criando Seu Primeiro Workflow no GitHub Actions

Criar seu primeiro workflow no GitHub Actions é um processo simples que envolve a definição de um arquivo YAML em seu repositório. Vamos passar pelos passos necessários para configurar um workflow básico que, por exemplo, executa testes em um projeto Node.js.

# Passo a Passo
1. **Crie um Repositório no GitHub**

Se ainda não tem um repositório, crie um novo:

1. Acesse GitHub.
2. Clique no botão "**New**" para criar um novo repositório.
3. Preencha os detalhes do repositório (nome, descrição, público/privado) e clique em "Create repository".

2. **Adicione o Código do Projeto**

Se você já tem um projeto, faça push do seu código para o repositório criado. Se não, pode iniciar com um projeto básico. Vamos assumir que você está trabalhando com um projeto Node.js.

    bash

    # No seu terminal
    mkdir my-first-workflow
    cd my-first-workflow
    npm init -y
    npm install jest --save-dev

    # Crie um arquivo de exemplo de teste
    echo "test('adds 1 + 2 to equal 3', () => {
    expect(1 + 2).toBe(3);
    });" > sum.test.js

    # Inicialize um repositório Git e faça o primeiro commit
    git init
    git add .
    git commit -m "Initial commit"
    # Adicione o repositório remoto
    git remote add origin https://github.com/<seu-usuario>/<nome-do-repositorio>.git
    git push -u origin main

3. **Crie o Workflow**

 - No seu repositório GitHub, vá para a aba "Actions".
 - Clique em "Set up a workflow yourself" ou "Configure" em um dos templates sugeridos.

4. **Defina o Workflow**

Crie um arquivo de workflow no caminho **.github/workflows/ci.yml**. Este arquivo YAML define o que o seu workflow fará.

    yaml

    name: CI Pipeline

    on:
    push:
        branches:
        - main
    pull_request:
        branches:
        - main

    jobs:
    build:
        runs-on: ubuntu-latest

        steps:
        - name: Check out the repository
            uses: actions/checkout@v2

        - name: Set up Node.js
            uses: actions/setup-node@v2
            with:
            node-version: '14'

        - name: Install dependencies
            run: npm install

        - name: Run tests
            run: npm test

# Explicação do Workflow

1. **Nome do Workflow**: **CI Pipeline**.
2. **Evento de Disparo**: O workflow é acionado em push e pull request no branch **main**.
3. **Job build**:
 - **runs-on**: Define que o job será executado em um runner **ubuntu-latest**.
 - **steps**:
  - **Checkout**: Faz o checkout do código do repositório.
  - **Setup Node.js**: Configura o Node.js na versão 14.
  - **Install dependencies**: Instala as dependências do projeto.
  - **Run tests**: Executa os testes definidos no projeto.

5. **Commit e Push do Workflow**

No seu terminal, commit e push do arquivo de workflow para o repositório GitHub.

    bash

    git add .github/workflows/ci.yml
    git commit -m "Add CI workflow"
    git push origin main

6. **Verifique a Execução do Workflow**

 - No GitHub, vá para a aba "Actions" do seu repositório.
 - Você verá o seu workflow CI Pipeline listado. Clique nele para ver os detalhes da execução.
 - Verifique se todos os jobs e steps foram executados com sucesso.

 # Conclusão

Você criou seu primeiro workflow no GitHub Actions! Agora, cada vez que você fizer um push ou criar um pull request para o branch **main**, os testes serão executados automaticamente. Esse é um passo importante para implementar práticas de CI/CD e garantir a qualidade contínua do seu código.

# Recursos Adicionais

    Documentação Oficial do GitHub Actions
    GitHub Actions Marketplace para encontrar ações reutilizáveis.
