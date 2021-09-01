# Anotações Git

### 1-Entendendo o que é Git e sua importância

- Ferramenta para controle de versionamento
- Criado em 2005
- Criado por Linus Torvalds
- Software é feito de forma colaborativa
- Github é o repositório online

### 2-Navegação via command line interface e instalação

- CLI- Command line interface
- GUI- Graphic user interface
- Mudar de pastas
  - cd ou cd
- Listar as pastas
  - dir ou ls
- Criar pastas/arquivos
  - mkdir
- Deletar aquivos
  - del
- Deletar pastas
  - rmdir
- Limpar terminal
  - cls ou clear
- Devolver uma mensagem no terminal
  - echo "mensagem"
- Criar arquivo com conteúdo
  - echo "mensagem" > nomedoarquivo.txt

### 3-Entendendo como o Git funciona por baixo dos panos

- SHA1
  - Secure Hash Algorithm - conjunto de funções hash criptográficas projetadas. Embaralhador e encriptador para identificar os arquivos de forma rápida.
    openssl sha1 "arquivo"
- Objetos fundamentais
  - BLOBS-Contem metadados e mais metadados do git como o tipo de objeto-o tamanho =-\0-Conteudo (Garda o SHA do arquivo)
  - TREES-Armazenam os blobs, é responsavel por montar toda a estrutura dos arquivos
  - COMMITS-Aponta para a Treem, para o Parent, para o Autor, Mensagem e timestamp.
    Qualquer alteração em qualquer arquivos os SHA´s de toda a cadeia serão ser alterados.
- Sistema distribuído
  As versões são compartilhadas entre todas as pessoas que estão trabalhando no projeto
  Segurança

### 4-Primeiros comandos com Git

- Iniciar o git
  - git init
-  Mostra arquivos ocultos
  - ls -a
- Inicializando pela primeira vez é necessário fazer algumas configurações
  - git config --global user.email ""
    git config --global user.name ""
- Iniciar o versionamento
  - git add
- Criar um commit
  - git commit

### 5-Ciclo de vida dos arquivos no Git

- Inicializa o repositório
  - git init
- Status dos arquivos
  - git status
- Tracked
  - Arquivos já adicionados
- Untracked para Staged
  - Estágio realizado pelo git add, onde o git passa a monitorar o aquivo
- Unmodified para Modified
  - O git compara a alteração do arquivo
- Modified para Staged
  - O git espera um git add para realizar o commit
- Staged para Unmodified
  - Quando é realizado o commit dos arquivos alterados
- Ciclo de vida
  - Unmodified -> Modified -> Staged
- Untracked
  - Arquivos ainda não adiconados
- Comando para mover
  - mv "nome do arquivo" caminho
    mv receitas.md ./receitas/
- git add
- git commit "mensagem"

### 6-Introdução ao GitHub

- Lista as configurações do Git
  - git config --global --list
- Remove a configuração
  - git config --global --unset

- Definir o repositório online
  - git remote add origin "endereço"
    origin é apenas um alias
- Exibir a lista de repositórios cadastrados
  - git remote -v
- Empurrar arquivos do diretório local para o repositório
  - git push origin mater

### 7-Resolvendo conflitos

- Conflito de merge
  - quando existe duas alterações na mesma linha
- Trazendo arquivos do repositório online para o local
  - git pull origin master

<<<<<<<<<<<<<<HEAD
O que estiver aqui é o que você alterou

________________________________________

Resolve conflitos manualmente

- git clone "url"
  - quando clona, já vem com o histórico de versionamento


​	