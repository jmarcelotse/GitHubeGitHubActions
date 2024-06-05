# Execução Paralela vs Sequencial de Jobs

No GitHub Actions, os jobs dentro de um workflow podem ser executados em paralelo ou de forma sequencial, dependendo de como você define as dependências entre eles. Entender como configurar e utilizar essas opções pode ajudar a otimizar o tempo de execução do seu workflow.

# Execução Paralela

Por padrão, todos os jobs em um workflow são executados em paralelo, a menos que você especifique uma dependência entre eles. A execução paralela é útil para tarefas independentes que podem ser realizadas simultaneamente, reduzindo o tempo total do pipeline.

# Exemplo de Execução Paralela

Aqui está um exemplo de um workflow com dois jobs (build e test) que são executados em paralelo:

    yaml

    name: Parallel Jobs Workflow

    on: [push]

    jobs:
        build:
            runs-on: ubuntu-latest

            steps:
                - name: Checkout code
                uses: actions/checkout@v2

                - name: Build application
                run: echo "Building the application..."

        test:
            runs-on: ubuntu-latest

            steps:
                - name: Checkout code
                uses: actions/checkout@v2

                - name: Run tests
                run: echo "Running tests..."

Neste exemplo, os jobs **build** e **test** começam a ser executados simultaneamente após um push.

# Execução Sequencial

Para que os jobs sejam executados de forma sequencial, você precisa definir dependências usando a palavra-chave needs. A execução sequencial é útil quando um job depende do resultado de outro.

# Exemplo de Execução Sequencial

Aqui está um exemplo de um workflow onde o job **deploy** depende do job **build** e só será executado após a conclusão do **build**:

# Combinando Execução Paralela e Sequencial

Você pode combinar a execução paralela e sequencial conforme necessário para otimizar o fluxo de trabalho. Por exemplo, você pode ter múltiplos jobs sendo executados em paralelo que depois convergem para um job final que depende deles.

**Exemplo de Execução Combinada**

Aqui está um exemplo onde **test** e **lint** são executados em paralelo, mas ambos precisam ser concluídos antes do job **deploy** iniciar:

    yaml

    name: Combined Jobs Workflow

    on: [push]

    jobs:
    build:
        runs-on: ubuntu-latest

        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Build application
            run: echo "Building the application..."

    test:
        runs-on: ubuntu-latest

        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Run tests
            run: echo "Running tests..."

    lint:
        runs-on: ubuntu-latest

        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Lint code
            run: echo "Linting code..."

    deploy:
        needs: [build, test, lint]
        runs-on: ubuntu-latest

        steps:
        - name: Checkout code
            uses: actions/checkout@v2

        - name: Deploy application
            run: echo "Deploying the application..."

Neste exemplo, **build**, **test**, e **lint** são executados em paralelo. O job **deploy** só começa após a conclusão bem-sucedida dos três jobs anteriores.

# Benefícios e Considerações

**Benefícios da Execução Paralela**

 - **Redução do Tempo Total**: Executar jobs em paralelo pode reduzir significativamente o tempo total do workflow.
 - **Eficiência**: Utiliza melhor os recursos disponíveis ao distribuir tarefas independentes.

**Benefícios da Execução Sequencial**

 - **Controle**: Garante que jobs dependentes sejam executados na ordem correta.
 - **Segurança**: Permite que você verifique resultados intermediários antes de prosseguir para a próxima etapa.

**Considerações**

 - **Dependências**: Certifique-se de definir claramente as dependências para evitar execuções desnecessárias.
 - **Recursos**: Jobs em paralelo podem consumir mais recursos simultaneamente. Verifique as limitações de recursos do seu plano no GitHub.
 - **Erro de Propagação**: Em execução sequencial, um erro em um job pode impedir a execução dos jobs subsequentes. Planeje a recuperação de falhas conforme necessário.

# Conclusão

Configurar a execução paralela e sequencial de jobs no GitHub Actions permite que você otimize o fluxo de trabalho de CI/CD para atender às necessidades do seu projeto. Ao combinar essas abordagens, você pode alcançar um equilíbrio entre eficiência e controle, garantindo que seu pipeline seja executado de forma rápida e confiável.

###

**needs**: [primeiro-job]  # Este job só será executado após a conclusão bem-sucedida do 'primeiro-job'