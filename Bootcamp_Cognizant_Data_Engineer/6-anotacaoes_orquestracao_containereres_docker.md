# Introdução a orquestração de contêineres com Docker

### 1-Introdução ao tema

### 2-Primeiros passos com o Docker

- Run
  - Criação do container com base na imagem
  - docker run --name newcontainer hello-world
    - docker run --name hello -d busybox sleep3600
      - docker run --name site -d -p 80:80 nginx (cria um container com nome site, no modo demo (-d), na porta 80 do servidor e com a porta 80 exposta pelo nginx (80:80))
  - curl localhost
    - Mostra o conteudo do localhost
  - netstat -nltp
    - Mostra as portas abertas do servidor
- ps
  - Listar os containeres
  - docker ps
- Info
  - Informações do docker
  - docker info (tras um sumario do que está sendo executado na máquina, e algumas informações da máquina)
- Images
  - Imagens utilizadas para criar os containeres
- Exec
  - Executar outro binario do container
  - docker exec hello mkdir teste (cria uma pasta chamada teste no container hello)
  - docker exec -it hello sh (acessa o container hello no modo iterativo)
  - exit (sai do container)
- Logs
  - Outputs e logs
  - docker logs site (mostra os logs do container site)
- Inspect
  - Listar todas as configurações do container
- Pull
  - Baixar imagens do repositorio
  - docker pull hello-world (baixa a imagem hello-world)
- Commit
  - Commitar modificações
  - docker commit --autor="" --message="Mensagem commit" hello hello (cria uma imagem com nome hello no container hello)
- Tag
  - Melhorar o versionamento
  - docker tag repositorioorigem usuario/repositorio:versao
    - docker tag hello micael/hello:1.0
  - 
- Login, logout
  - Logar no repositorio
- Push
  - Compartilhar ou armazenar a imagens no repositorio
- Search
  - Procurar imagem
- RM
  - Remover container
- RMI
  - Remover imagem
- Export, Import
  - Exportar ou importar container
- Save, Load
  - Salvar ou carregar uma imagem
- Dive
  - Mostra as camadas do container
- A partir da imagem busybox criou-se o container hello, que por sua vez criou a imagem hello



### 3-Rede do Docker

- docker network sl
  - Exibe as conexoes da instancia
- Bridge
  - Rede default do Docker, utilizado para comunicação entre containers
  - Pode se definir o range de IPs no momento de criação da rede
  - Permite comunicação do container para rede, internet e outros containers
  - ![image-20210914111346625](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210914111346625.png)
  - docker network create -d bridge petsBridge
    - cria uma conexão tipo bridge com o nome petsBridge
  - docker run -d --net petsBridge --name db consul
    - criar um container em modo demo na conexão petsBridge com o nome db utilizando a imagem consul
  - docker run -d --env "DB=db" --net petsBridge --name web -p 8000:5000 chrch/docker-pets:1.0
    - cria um container em modo demo 
    - atribui a variavel ambiente DB ao db
    - adiciona na rede petsBridge
    - nome web
    - expoe a porta 8000 do servidor que a aplicação está ouvindo 
    - mapeando a porta 5000 que a onde a aplicação foi criada
    - imagem chrch/docker-pets:1.0
- Host
  - remove o isolamento de rede, o container responde diretamente pela placa de rede do host
  - Recebem o mesmo Ip do Host fisico
  - Não é possivel expor uma porta em que o Host estiver usando
  - Utiliza a mesma placa física de rede
  - ![image-20210914111449587](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210914111449587.png)
  - docker run -d --net host --name db consul
    - criar um container em modo demo na conexão host com o nome db utilizando a imagem consul
  - docker run -d --env "DB=localhost" --net host --name web chrch/docker-pets:1.0
    - cria um container em modo demo 
    - atribui a variavel ambiente DB ao localhost
    - adiciona na rede host
    - nome web
    - a porta é a aplicação que define
    - imagem chrch/docker-pets:1.0
- Overlay
  - Permite comunicação entre containeres de host (vms) diferentes
  - Criação de um docker swarm
  - Melhore escabilidade dos hosts e dos containeres
  - ![image-20210914111750682](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210914111750682.png)
  - para fazer a criação de uma comunicação entre dois containeres em hosts diferentes é necessário um cluster de swarm(kubernets)
  - cluster de swarm
    - um dos hosts deve ser o principal
    - porta 4789
    - docker swarm init --advertise-addr 192.168.0.18
      - cria o cluster no servidor 192.168.0.18
      - gera um token para inserir nos outros hosts
    - docker node ls
      - lista as conexoes com outros servidores
  - docker network create -d overlay petsOverlay
    - cria uma conexao overlay em modo demo com o nome petsOverlay
  - docker service create --network petsOverlay --name db consul
    - cria um serviço overlay nomeado db com consul
  - docker service create --network petsOverlay -p 8000:5000 -e 'DB-db' --name web chrch/docker-pets:1.0
  - docker service scale web=3
    - escala os serviços para 3 servidores
- Macvlan
  - Permite atribuir um endereço MAC ao container tornando ele visível como um dispositivo físico na rede
- None
  - Sem rede
- Repositorio
  - https://github.com/luistkd4/docker101

### 4-Armazenamento no docker

![](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210914192131979.png)

- Volume
  - disco virtual onde o docker engine tem total autonomia sobre ele
  - o host não precisa ter uma estrutura de arquivos
  - torna mais carregado a leitura do disco
  - preferível para usar em ambientes replicados
  - se o container é removido as informações são persistidas em disco
- Bind mounts
  - Pasta compartilhada com o container
  - se o container é removido as informações são persistidas em disco
- tmpfs mounts
  - armazenamento temporário
  - logs de aplicação
  - 

