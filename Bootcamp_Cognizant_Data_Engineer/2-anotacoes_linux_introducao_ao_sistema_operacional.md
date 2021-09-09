# Anotações Introdução Linux

### 1-Introdução ao Linux e configuração inicial

- Criado em 1991 por Linus Torvals
- O linux é o Kernel, o que da vida ao sistema operacional
  - Hardware->Kernel->Shell
- É desenvolvida por diversas pessoas e empresas ao redor do mundo
- É multitarefa e multiusuário
- Existe distribuição linux para qualquer aplicação
- Ubuntu-sistema operacional de código aberto que é desenvolvido pela Canonical com base no kernel linux, tem base no Debian.
- VMware Worksation 15
- Ubuntu v.20.4
- Doca é a barra de tarefas ao lado esquerdo, parecida com o gerenciador de tarefas do windows
- A pasta raíz é a barra
- Ubuntu software
  - Loja de aplicações linux

### 2-Conhecendo o terminal Linux e seus atalhos

- Terminal, shell ou konsole
  - podemos executar programas específicos Linux
  - uso para automação de processos através de comandos
  - pode ser aberto por CTRL + ALT + T
- Os comandos são iguais em diversas distribuições
- ~ significa que está na pasta usuário, pasta de trabalho
- pwd
  - exibe o caminho local
- ls
  - listagem de arquivos e diretórios
- la -a
  - mostras os arquivos e diretórios em oculto
- ls "Nome da pasta"
  - lista os arquivos que existe dento da pasta especificada
- ls -l
  - lista os itens com detalhes (restrições, usuário, tamanho, mes de criação, data de criação, hora de criação)
- cd "Nome da pasta"
  - Troca o diretório para a pasta especificada
- mkdir "Nome da pasta"
  - cria pasta
- cd ..
  - volta para o diretório anterior
- cd /
  - redireciona para o diretório raiz, c:
- man "comando"
  - retorna o manual do comando, exemplo: man ls
  - para retornar ao terminal, pressionar "q"
- "comando" --help
  - retorna o manual com comando em portugues na maioria das vezes
  - para retornar ao terminal, pressionar "q"
- cd ~
  - voltar para o diretório pessoal
- history
  - exibe o histórico de comandos do terminal
  - comando -c: limpa o histórico
- !!
  - executa o ultimo comando do terminal
- Atalhos
  - ![image-20210901102719495](C:\workspace\anotacoes_aulas\img\image-20210901102719495.png)
- mv "Caminho"
  - Move o arquivo
    - mv "Nome inicial do arquivo" "Nome futuro" 
    - mv Teste Linux
  - Renomea o arquivo
    - mv "Nome inicial do arquivo" "Caminho futuro" 
    - mv Linux ~ 
- touch
  - cria arquivos vazios sem conteúdo
    - touch teste.txt
- cp
  - copia o arquivo
    - cp "nome do arquivo" "caminho"
    - cp linux.txt /home/bruno
- Tab
  - autocompleta
- clear ou CTRL+L
  - limpa o terminal
- rmdir
  - remove o diretório
  - rmdir Linux
- rm
  - remove arquivos
  - rm Teste.txt
- exit ou CTRL + D
  - sai do terminal
- Revisão de comandos
  - ![image-20210901104339264](C:\workspace\anotacoes_aulas\img\image-20210901104339264.png)

### 3-Comandos para manipulação de arquivos e textos e redirecionamento

- nano
  - editor de texto em terminal do ubuntu linux
- ^
  - é o CTRL
- M
  - é o ALT
- CTRL + O
  - Salva o arquivo
- CTRL + X
  - Sai do nano
- cat "nome do arquivo"
  - Abre o conteudo do arquivo no terminal
- tac "nome do arquivo"
  - Abre o conteúdo com as linhas invertidas no terminal
- head "nome do arquivo"
  - Exibe as primeiras 10 linhas do arquivo
- tail "nome do arquivo"
  - Exibe as ultimas 10 linhas do arquivo
- ">"
  - Cria um arquivo contendo as informações
  - Exemplo: tail teste.txt > distros.txt
- cal
  - Exibe o calendário do mês corrente no terminal
- cal "Ano"
  - Exibe os calendários do ano no terminal
- date
  - Exibe a data de hoje
- ">>"
  - Adiciona o conteúdo ao arquivo
  - Exemplo: date >> calendario_jul.txt
- grep
  - Realiza busca dentro do arquivo
- "| "
  - Possibilita concatenar comandos no terminal
  - Exemplo: tail distros.txt | grep linux -> Realiza a busca da palavra linux nas ultimas dez linha do arquivo distros.txt
- "|" more
  - Realiza uma paginação na exibição do conteudo, ao pressionar ENTER
- "|" less
  - Realiza uma paginação na exibição do conteudo, ao pressionar ENTER
- "&"
  - Separa por linha de comando o resultado
  - Exemplo: cat teste.txt & cat teste2.txt
- "&&"
  - Executa os comandos em consecutivo, sem pausa entre linhas de comando
  - Exemplo: mkdir linux_ubutu && cd linux_ubuntu -> cria a pasta "linux_ubuntu" e navega até ela
- file
  - demonstra qual é o tipo de arquivo
- whatis
  - exibe o que realiza o comando
  - Exemplo: whatis file
- find
  - procura o arquivo dentro de um determinado lugar
  - Exemplo: find ~ -name maio.txt -> Procura na pasta pessoal ~ pelo nome o arquivo maio.txt

### 4-Diretórios do Linux e comandos de sistema

- Diretórios
  - ![image-20210901161434254](C:\workspace\anotacoes_aulas\img\image-20210901161434254.png)
- Binários
  - São os executáveis do Linux
- root
  - É o super usuário do sistema
- cpuinfo ou lscpu
  - Exibe as informações de processador
- meminfo
  - Exibe as informações de memória do sistema
- free
  - Exibe os status de memória
    - SWAP: memória virtual do sistema
- lspci
  - Exibe todos as placas conectadas no computador
- lsusb
  - Exibe todos os equipamentos que estão conectados por USB
- arch
  - Exibe a arquitetura do kernel do sistema
- uname
  - Exibe o nome do Kernel
- uname -r
  - Exibe a versão do kernel
- du -h "diretório"
  - Exibe o quanto do diretório ocupa de HD
  - Exemplo: du -h ~ -> exibe quanto o diretório pessoal ocupa do HD
- cat /etc/passwd
  - Exibe todos os usuário do sistema
- reboot
  - Reinicia o sistema
- shutdown -h "tempo"
  - Desliga o sistema
- lshw
  - Lista de todos os hardwares

### 5-Fundamentos de rede e comandos de rede

- Rede
  - conjunto de equipamentos interligados para trocar informações e compartilhar recursos
- Nós
  - São os pontos de rede
- WAN (Wide Area Network)
  - uma rede geograficamente distribuída, liga continentes
- MAN (Metropolitan Area Network)
  - rede metropolitana
- LAN (Local Area Netowork)
  - rede local em um unico local (prédio, campus)
- Protocolos
  - linguagem usada pelos dispositivos de uma rede para que eles consigam se entender
  - IP (Internet protocol)
    - numeros que identificam o dispositivo em uma rede
  - ICMP (Internet Control Message Protocol)
    - prover mensagens de controle na comunicação entre nós
  - DNS (Domain Name Server)
    - protocolo de aplicação, identificar endereços IP´s, manter uma tabela com os endereços dos caminhos de algumas redes
- Interface de rede
  - software ou hardware que faz a comunicação em uma rede de computadores
- Loopback
  - interface que permite fazer conexões com você mesmo
- ifconfig (pacote net tools)
  - exibe as informações de ip
- sudo
  - faz elevação de priviégio para administrador
- inet
  - endereço na rede local
- netmask
  - número 32 bits, que separa a rede publica da rede privada
- broadcast
  - endereço publico da rede local
- inet6
  - surgiu pela quantidade de computadores que existem no mundo
- ehter
  - endereço MAC, endereço da placa de rede, único
- hostname
  - tras informações sobre o host
- hostname -I
  - endereço IP
- hostname -I
  - endereço de loopback
- who
  - como está logado na rede
- whoami
  - nome do usuário logado na rede
- ping
  - faz parte do protocolo ICMP
  - verifica se o host está ativo, enviando pacotes de requisições para o host
- dig
  - tras informações do DNS
  - +short: trás somente a informação de IP do host

- DNS
  - serviço de domínio de nomes
- tracerout
  - retorna a rota de nós até chegar em determinado host
- whois
  - trás mais informações sobre determinado host
- finger
  - mostra toda a informação do usuário logado no host

### 6-Fuçando no Linux com comandos diversos

- alias
  - determina um apelido ao um comando
  - exemplo: alias hh='history'
- nl
  - conta o numero de linhas de um arquivo
- wc -l
  - conta o numero de linhas de um arquivo, considerando as linhas em branco
  - exemplo: wc -l nome.txt
- wc -w
  - conta o numero de palavras de um arquivo
  - exemplo: wc -w nome.txt
- cmp
  - faz comparação entre arquivos
- diff
  - mostra a diferença entre os arquivos
- sort
  - organiza a saida do conteúdo do arquivo no terminal
- last reboot
  - todas as informações de reinicialização do sistema
- route
  - mostrará todas as tabelas de roteamento do Kernel
- time
  - calcula o tempo do processo do comando
  - exemplo: time traceroute www.google.com.br

- uptime
  - tempo que o sistema está rodando
- init 0
  - desliga a maquina
- telinit 0
  - desliga a maquina
- seq
  - imprimi a sequencia de caracteres
  - exemplo: seq 1 10
- Comandos
  - ![image-20210903140834343](C:\workspace\anotacoes_aulas\img\image-20210903140834343.png)

### 7-Controle de usuários, grupos e permissões

- root

  - é o usuário que possui todas as permissões no Linux

- adduser

  - adiciona um usuário
  - exemplo: adduser nomedousuario

- su

  - troca o usuario do terminal
  - exemplo: su novousuario

- passwd

  - altera a senha do usuário
  - exemplo: passwd nomeusuario
  - cat etc/paswwd : exibe todos os usuários

- last

  - exibe as informações de login dos usuarios de todo o sistema

- logname

  - exibe o nome do usuário atual do sistema

- id

  - exibe todos os identificadores dos usuarios

- userdel -r 

  - remove o usuário
  - -r remove a pasta pessoal

- Grupos

  - permitem orgainzar os usuários e definir as permissões de acesso a arquivos.
  - cat /etc/group
    - exibe todos os grupos do sistema

- groups

  - exibe todos os grupos de um usuário

- adadgroup

  - cria um grupo

- adduser

  - adiciona um usuário ao grupo
  - exemplo: adduser nomeusuario nomegrupo

- gpasswd -a

  - adiciona um usuário ao grupo
  - exemplo: gpasswd -a nomeusuario nomegrupo

- gpasswd -a

  - remove um usuário de um grupo

- Permissões

  - servem para restringir acessos de leitura, escrita e execução em arquivos e diretórios
  - r-read
  - w-write
  - x-execution

- ls -lh

  - mostra detalhes
  - d rwx rwx rwx - primeira sequencia é o dono, segunda sequencia quem pertence ao grupo e terceira sequencia os outros
    - ![image-20210903145150407](C:\workspace\anotacoes_aulas\img\image-20210903145150407.png)

- chmod

  - muda permissão de um arquivo ou diretório
  - exemplo: chmod 700 nomedoarquivo.txt

- Modo octal

  - ![image-20210903145450763](C:\workspace\anotacoes_aulas\img\image-20210903145450763.png)

  ### 8-Compactação, descompactação e arquivamento

- gzip

  - compacta um arquivo
  - -9 compactação máxima
  - exemplo: gzip nomearquivo.txt

- gunzip

  - descompacta o arquivo
  - exemplo: gunzip nomearquivo.txt.gz

- zip

  - exemplo: zip nomedoarquivo.zip nomearquivocompactar.txt

- unzip

  - exemplo: unzip arquivo.zip

- bzip2

  - mais atual que os outros
  - exemplo: bzip2 nomearquivo.txt

- bzip2 -d

  - descompacta arquivo
  - exemplo: bzip2 -d arquivo.bz2

- rar a

  - exemplo: rar a arquivo.rar nomearquivo.txt

- rar z

  - descompacta arquivo
  - exemplo: rar x arquivo.rar

- Arquivadores

  - Junta varios arquivos em um só, pode ser usado em conjunto com compactadores

- tar -cf

  - exemplo: tar -cf arquivos.tar arquivo1.txt arquivo2.txt arquivo3.txt

- tar -xvf

  - exemplo mesmo diretório: tar -xvf arquivos.tar.gz
  - exemplo outro diretório: tar -xvf arquivos.tar.gz -C ~/Documentos

  ### 9-Gerenciamento de pacotes

- Pacotes

  - são programas dentro de um arquivo identificados por sua extensão, e incluem arquivos necessário para a instalação de programa
  - .deb, .rpm

- Gerenciadores de pacotes

  - são sistemas que possuem resolução automática de dependências entre pacotes, metrodo fácil de instalação de pacotes
  - dpkg, apt, yurn

- APT

  - sudo apt install
    - instala
  - sudo apt upgrade
    - atualiza
  - sudo apt remove
    - remove pacote
  - sudo apt update && apt upgrage
    - atualiza o sistema
  - dpkg
    - outro gerenciador de pacotes do tipo .deb
    - sudo dpkg -i nomearquivo.deb
      - instala
    - sudo dpkg -i nomearquivo.deb
      - descrição do pacote
    - sudo dpkg -r nomearquivo
      - remove o pacote, sem .deb, descrição que consta na descrição Package

- RPM

  - sudo rpm -IVH nomearquivo.rpm
    - instala
    - --nodeps ,instala as dependencias
  - sudo rpm -U nomearquivo.rpm
    - atualiza
  - sudo rpm -e nomearquivo.rpm
    - remove

- YUM

  - sudo yum install pacote
    - instala o pacote
  - sudo yum update pacote
    - atualiza o pacote
  - sudo youm remove pacote
    - remove o pacote



