# Usando Actions

# Usando GitHub Actions

GitHub Actions permite que você automatize seu fluxo de trabalho de desenvolvimento de software diretamente no GitHub. Vamos explorar como usar o GitHub Actions com exemplos práticos, desde a configuração básica até a utilização de ações personalizadas e de terceiros.

**Passo 1: Criação do Repositório**

1. **Crie um Repositório no GitHub**:
    - Acesse GitHub.
    - Clique em "New" para criar um novo repositório.
    - Preencha os detalhes do repositório e clique em "Create repository".

**Passo 2: Clonar o Repositório**

Clone o repositório recém-criado para sua máquina local.

    bash

    git clone https://github.com/<seu-usuario>/<nome-do-repositorio>.git
    cd <nome-do-repositorio>

**Passo 3: Adicionar Código ao Repositório**

Vamos criar um exemplo simples de projeto Node.js com Jest para testes.

**Iniciar um Projeto Node.js**

    bash

    npm init -y
    npm install jest --save-dev

**Adicionar um Arquivo de Test**e

Crie um arquivo de teste chamado **sum.test.js**.

    javascript

    test('adds 1 + 2 to equal 3', () => {
    expect(1 + 2).toBe(3);
    });

**Passo 4: Commit e Push do Código**

Adicione, commite e faça push do código para o repositório GitHub.

    bash

    git add .
    git commit -m "Initial commit"
    git push origin main

**Passo 5: Configurar o Workflow no GitHub Actions**

1. **Acesse a Aba "Actions"**:
    - No repositório GitHub, vá para a aba "Actions".

2. **Configure um Novo Workflow**:
    - Clique em "Set up a workflow yourself" ou escolha um template sugerido.
    - Crie um arquivo chamado ci.yml no diretório .github/workflows/.

**Exemplo de Workflow**

Aqui está um exemplo de workflow básico para um projeto Node.js.

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

**Passo 6: Commit e Push do Workflow**

Adicione e faça o commit do arquivo de workflow.

    bash

    git add .github/workflows/ci.yml
    git commit -m "Add CI workflow"
    git push origin main

**Passo 7: Verificar a Execução do Workflow**

1. Acesse a Aba "Actions":
    - No GitHub, vá para a aba "Actions" do seu repositório.

2. Verifique o Status do Workflow:
    - Você verá o workflow CI Pipeline listado. Clique nele para ver os detalhes da execução.
    - Verifique se todos os jobs e steps foram executados com sucesso.

# Usando Ações de Terceiros

Você pode usar ações pré-construídas do GitHub Marketplace para estender seu workflow.

**Exemplo de Ação de Terceiro**

Vamos adicionar uma ação para verificar a formatação do código com o Prettier.

 1. **Adicionar uma Nova Etapa no Workflow:**

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

            - name: Run Prettier
            uses: creyD/prettier_action@v3.1
            with:
            prettier_options: --write **/*.js

            - name: Run tests
            run: npm test

# Criando Ações Personalizadas

Você pode criar suas próprias ações para reutilizar em diferentes workflows.

**Exemplo de Ação Personalizada**

1. **Criar um Diretório para a Ação**:
    - Crie um diretório chamado **my-action** no seu repositório.

2. **Adicionar um Arquivo de Ação**:
    - Crie um arquivo **action.yml** dentro do diretório **my-action**.

    yaml

    name: 'My Custom Action'
    description: 'An example action to greet someone'
    inputs:
        name:
            description: 'The name of the person to greet'
            required: true
    runs:
        using: 'node12'
        main: 'index.js'

3. **Adicionar o Código da Ação**:
    - Crie um arquivo **index.js** dentro do diretório **my-action**.

    javascript

    const core = require('@actions/core');

    try {
    const name = core.getInput('name');
    console.log(`Hello ${name}!`);
    } catch (error) {
    core.setFailed(error.message);
    }

4. **Adicionar Dependências da Ação**:
    - Crie um arquivo **package.json** dentro do diretório **my-action**.

    json

    {
        "name": "my-action",
        "version": "1.0.0",
        "main": "index.js",
        "dependencies": {
            "@actions/core": "^1.2.6"
        }
    }

5. **Commit e Push da Ação**:
    - Adicione, commit e faça push dos arquivos da ação.

    bash

    git add my-action
    git commit -m "Add custom action"
    git push origin main

# Usar a Ação Personalizada no Workflow

Atualize o workflow para usar a ação personalizada.

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

      - name: Run custom action
        uses: ./my-action
        with:
          name: 'World'

      - name: Run tests
        run: npm test

# Conclusão

GitHub Actions é uma ferramenta poderosa para automatizar fluxos de trabalho de desenvolvimento. Ao seguir estes passos, você pode configurar e utilizar workflows automatizados, usar ações de terceiros do GitHub Marketplace e até criar suas próprias ações personalizadas. Isso não só melhora a eficiência do desenvolvimento, mas também ajuda a manter a qualidade do código através de integração e entrega contínuas.

######

https://github.com/marketplace

segundo-job:
    name: "Instalação do Ambiente NodeJS"
    runs-on: ubuntu-latest  # O job será executado em uma máquina virtual com o Ubuntu mais recente
    needs: [primeiro-job]  # Este job só será executado após a conclusão bem-sucedida do 'primeiro-job'
    steps:
       - name: "Verificação da versão do NodeJS atual"
         run: node --version  # Verifica e exibe a versão atual do NodeJS instalada na máquina
       - name: "Definição da versão 20.13.1 do NodeJS"
         uses: actions/setup-node@v4.0.2  # Utiliza a ação 'setup-node' para instalar a versão especificada do NodeJS
         with:
          node-version: '20.13.1'  # Especifica a versão 20.13.1 do NodeJS a ser instalada
       - name: "Verificação da versão do NodeJS depois de instalar"
         run: node --version  # Verifica e exibe a versão do NodeJS após a instalação da nova versão