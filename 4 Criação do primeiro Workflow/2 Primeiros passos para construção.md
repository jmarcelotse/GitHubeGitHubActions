# Primeiros Passos para Construir um Workflow com GitHub Actions

Vamos detalhar os primeiros passos para construir e executar um workflow no GitHub Actions, passo a passo, desde a criação de um repositório até a configuração do primeiro workflow.

# Passo 1: Crie um Repositório no GitHub

1. Acesse o GitHub:
 - Vá para GitHub.

2. **Crie um Novo Repositório**:
 - Clique no botão "New" para criar um novo repositório.
 - Preencha os detalhes necessários, como nome do repositório, descrição e visibilidade (público/privado).
 - Clique em "Create repository".

# Passo 2: Clone o Repositório Localmente

Clone o repositório recém-criado para sua máquina local.

    bash

    git clone https://github.com/<seu-usuario>/<nome-do-repositorio>.git
    cd <nome-do-repositorio>

# Passo 3: Adicione o Código do Projeto

Se você já tem um projeto, copie seu código para dentro do diretório clonado. Caso contrário, você pode iniciar um novo projeto. Aqui, vamos criar um exemplo simples com Node.js.

    bash

    # Inicialize um novo projeto Node.js
    npm init -y

    # Instale uma biblioteca de teste, como o Jest
    npm install jest --save-dev

    # Adicione um script de teste no package.json
    # Adicione a linha `"test": "jest"` no campo "scripts"

**Exemplo de package.json:**

    json

    {
    "name": "my-first-workflow",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
    "test": "jest"
        },
    "devDependencies": {
        "jest": "^27.0.0"
        }
    }

**Adicione um Arquivo de Teste**

Crie um arquivo de teste, como sum.test.js:

    javascript

    test('adds 1 + 2 to equal 3', () => {
    expect(1 + 2).toBe(3);
    });

# Passo 4: Commit e Push do Código

Adicione o código ao repositório Git e faça o push para o GitHub.

    bash

    git add .
    git commit -m "Initial commit"
    git push origin main

# Passo 5: Configure o Workflow no GitHub Actions

1. **Acesse a Aba "Actions"**:
 - No seu repositório GitHub, vá para a aba "Actions".

2. **Configure um Novo Workflow**:
 - Clique em "Set up a workflow yourself" ou escolha um template sugerido.
 - Nomeie o arquivo como **ci.yml** e coloque-o no diretório **.github/workflows/**.

**Exemplo de Workflow**

Crie o arquivo **.github/workflows/ci.yml** com o seguinte conteúdo:

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

# Passo 6: Commit e Push do Workflow

Adicione e faça o commit do arquivo de workflow.

    bash

    git add .github/workflows/ci.yml
    git commit -m "Add CI workflow"
    git push origin main

# Passo 7: Verifique a Execução do Workflow

1. **Acesse a Aba "Actions"**:
 - No GitHub, vá para a aba "Actions" do seu repositório.

2. **Verifique o Status do Workflow**:
 - Você verá o workflow **CI Pipeline** listado. Clique nele para ver os detalhes da execução.
 - Verifique se todos os jobs e steps foram executados com sucesso.

# Conclusão

Você configurou seu primeiro workflow no GitHub Actions! Este workflow agora será executado automaticamente em cada push ou pull request para o branch **main**, executando testes para garantir a qualidade contínua do seu código.

# Recursos Adicionais

 - Documentação do GitHub Actions: Guia completo sobre como configurar e usar o GitHub Actions.
 - GitHub Actions Marketplace: Ações pré-construídas que você pode usar para estender seu workflow.
 - Tutoriais e Exemplos: Explore tutoriais e exemplos para aprender mais sobre as capacidades do GitHub Actions.

Com esses passos, você deve estar bem equipado para começar a construir e personalizar workflows no GitHub Actions para atender às necessidades do seu projeto.

###

1. Repositorio
2. Actions
3. New workflow
4. set up a workflow yourself
5. Editar
6. Commit