# Criando Seu Primeiro Projeto de Pipeline no GitHub Actions

Vamos criar um projeto simples com um pipeline básico usando GitHub Actions. Este exemplo usará Node.js, mas os conceitos podem ser aplicados a qualquer linguagem ou stack de tecnologia.

# Passo a Passo para Criar o Pipeline
**Passo 1: Criar um Novo Repositório no GitHub**

1. **Acesse GitHub**:
    - Vá para GitHub.

2. **Crie um Novo Repositório**:
    - Clique em "New" para criar um novo repositório.
    - Dê um nome ao repositório, por exemplo, my-first-pipeline.
    - Defina a visibilidade (público ou privado) e clique em "Create repository".

**Passo 2: Clonar o Repositório Localmente**

Clone o repositório para a sua máquina local.

    bash

    git clone https://github.com/<seu-usuario>/my-first-pipeline.git
    cd my-first-pipeline

**Passo 3: Adicionar Código ao Projeto**

Vamos criar um simples projeto Node.js com Jest para testes.

1. Inicializar um Projeto Node.js:

    bash

    npm init -y
    npm install jest --save-dev

2. Adicionar um Arquivo de Teste:

Crie um arquivo **sum.test.js** no diretório raiz do projeto com o seguinte conteúdo:

    javascript

    // sum.test.js
    test('adds 1 + 2 to equal 3', () => {
    expect(1 + 2).toBe(3);
    });

3. Configurar o Script de Teste no **package.json**:

Abra o arquivo **package.json** e adicione o script de teste:

    json

    {
    "name": "my-first-pipeline",
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

**Passo 4: Commit e Push do Código**

Adicione, faça commit e push do código para o repositório no GitHub.

    bash

    git add .
    git commit -m "Initial commit with basic Node.js project and Jest tests"
    git push origin main

**Passo 5: Configurar o Workflow do GitHub Actions**

1. **Acessar a Aba "Actions"**:
    - No seu repositório GitHub, vá para a aba "Actions".

2. **Configurar um Novo Workflow**:
    - Clique em "Set up a workflow yourself" ou escolha um template sugerido.
    - Nomeie o arquivo como ci.yml e coloque-o no diretório **.github/workflows/**.

3. Definir o Workflow:

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
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Set up Node.js
            uses: actions/setup-node@v2
            with:
            node-version: '14'

        - name: Install dependencies
            run: npm install

        - name: Run tests
            run: npm test

**Passo 6: Commit e Push do Workflow**

Adicione, faça commit e push do arquivo de workflow.

    bash

    git add .github/workflows/ci.yml
    git commit -m "Add CI workflow for Node.js project"
    git push origin main

**Passo 7: Verificar a Execução do Workflow**

1. Acessar a Aba "Actions":
    - No GitHub, vá para a aba "Actions" do seu repositório.

2. Verificar o Status do Workflow:
    - Você verá o workflow CI Pipeline listado. Clique nele para ver os detalhes da execução.
    - Verifique se todos os jobs e steps foram executados com sucesso.

# Benefícios do Pipeline

- **Automação**: Cada push e pull request dispara o pipeline, automatizando a execução de testes.
- **Qualidade**: Garante que os testes sejam executados sempre que o código é alterado.
- **Feedback Rápido**: Proporciona feedback imediato sobre o estado do código.

# Expansão do Pipeline

Uma vez que o pipeline básico esteja funcionando, você pode expandi-lo para incluir:

- **Linters**: Adicione passos para verificar a formatação e padrões de código.
- **Builds**: Compile o código ou gere artefatos de build.
- **Deploys**: Automatize o deploy do código para diferentes ambientes.
- **Testes Avançados**: Execute testes de integração e end-to-end.

# Exemplo de Expansão

Adicionando um passo para executar o ESLint:

1. **Instalar o ESLint**:

    bash

    npm install eslint --save-dev

2. **Configurar o ESLint**:

Crie um arquivo .eslintrc.json com a configuração básica:

    json

    {
    "env": {
        "browser": true,
        "es2021": true,
        "node": true
    },
    "extends": "eslint:recommended",
    "parserOptions": {
        "ecmaVersion": 12,
        "sourceType": "module"
    },
    "rules": {
    }
    }

3. **Atualizar o Workflow**:

Atualize o arquivo **.github/workflows/ci.yml** para incluir o ESLint:

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
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Set up Node.js
            uses: actions/setup-node@v2
            with:
            node-version: '14'

        - name: Install dependencies
            run: npm install

        - name: Run ESLint
            run: npx eslint .

        - name: Run tests
            run: npm test

# Conclusão

Você criou com sucesso seu primeiro pipeline de CI usando GitHub Actions. Este pipeline básico pode ser expandido para incluir verificações de qualidade de código, builds e deploys, permitindo que você automatize e melhore continuamente seu fluxo de trabalho de desenvolvimento.
