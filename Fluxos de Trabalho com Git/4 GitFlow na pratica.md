1. Criar um repositorio

    mkdir gitflow

    cd gitflow/

    git init

<<<<<<< Updated upstream
    git branch -m develop
=======
    git branch -m develop

    go mod init jmarcelotse/gitflow

Criar o arquivo main.go

    go run main.go

    git add .

    git checkout -b feature/feature-xpto

Ajusta o codigo

    git status

    git add .

Jogar agora para develop

    git checkout develop

    git branch

    git merge feature/feature-xpto

Criar o release

    git checkout -b release

    git checkout -b main

    git merge release
>>>>>>> Stashed changes
