# Runners

Documentação do Runners: https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources

Os runners são instâncias de máquinas virtuais, contêineres Docker ou hosts físicos usados para executar jobs em workflows do GitHub Actions. Eles são responsáveis por executar as etapas definidas nos workflows e fornecer o ambiente de execução necessário para as tarefas específicas do job.

# Tipos de Runners

Existem dois tipos principais de runners usados no GitHub Actions:

1. **Runners Hospedados (Hosted Runners)**:

    - São mantidos e provisionados pelo GitHub.
    - Disponibilizados em diferentes sistemas operacionais, como Ubuntu, Windows e macOS.
    - O GitHub fornece várias opções de configuração, como tamanho da máquina, poder de computação e software pré-instalado.

2. **Runners Auto-hospedados (Self-hosted Runners)**:

    - São executados em sua própria infraestrutura, como máquinas virtuais, contêineres ou servidores físicos.
    - Você precisa configurar e gerenciar esses runners por conta própria.
    - Permitem maior controle sobre o ambiente de execução e podem ser personalizados de acordo com suas necessidades específicas.

# Funcionamento dos Runners

Quando um workflow é acionado (por exemplo, após um push para o repositório), o GitHub Actions seleciona um runner disponível para executar os jobs do workflow. O runner baixa o código-fonte do repositório, executa as etapas definidas no job e relata o resultado de volta ao GitHub.

# Uso de Runners no GitHub Actions

Os runners são essenciais para o funcionamento do GitHub Actions e são responsáveis por garantir a execução confiável e eficiente dos workflows. Aqui estão algumas considerações importantes sobre o uso de runners:

 - **Disponibilidade**: O GitHub Actions gerencia automaticamente os runners hospedados, garantindo que haja capacidade suficiente para lidar com a carga de trabalho dos workflows.
 - **Customização**: Com runners auto-hospedados, você tem controle total sobre o ambiente de execução e pode personalizá-lo para atender às necessidades específicas do seu projeto.
 - **Escala**: Os runners hospedados podem dimensionar automaticamente para lidar com grandes volumes de jobs, enquanto os runners auto-hospedados requerem gerenciamento manual para escalar conforme necessário.
 - **Segurança**: Os runners auto-hospedados exigem atenção especial à segurança para garantir que apenas usuários autorizados tenham acesso à infraestrutura.

# Conclusão

Os runners são componentes fundamentais do GitHub Actions, fornecendo o ambiente de execução necessário para executar os workflows. Seja usando runners hospedados pelo GitHub ou implementando seus próprios runners auto-hospedados, é importante entender como esses recursos funcionam e como podem ser usados para otimizar o processo de desenvolvimento e implantação de software.


################################
