# Variáveis

# Variáveis no GitHub Actions: Conceito e Configuração

No GitHub Actions, variáveis são valores que você pode definir e reutilizar em diferentes workflows. Elas são úteis para armazenar informações que são usadas frequentemente ou que podem mudar dependendo do ambiente, como URLs de banco de dados, nomes de ambientes, ou qualquer outro valor que você precise acessar em seus jobs.

# Conceito de Variáveis

- **Variáveis**: São valores que você pode definir e acessar em seus workflows. Elas podem ser usadas para armazenar dados constantes que você precisa reutilizar em vários lugares.
- **Segredos**: São variáveis especiais que contêm informações sensíveis, como tokens de API ou senhas. Segredos são criptografados e não são exibidos nos logs dos workflows.

# Níveis de Definição de Variáveis

1. **Nível de Repositório**:
    - As variáveis definidas no nível do repositório estão disponíveis para todos os workflows dentro desse repositório específico.
    - Elas podem ser usadas para armazenar configurações que são específicas para um projeto.

2. **Nível de Organização**:
        As variáveis definidas no nível da organização estão disponíveis para todos os repositórios dentro dessa organização.
        Elas são úteis para configurações comuns que precisam ser compartilhadas entre vários projetos.