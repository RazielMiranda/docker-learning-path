
<img src="docker-ferramenta-para-dev.jpg">

curso: https://www.udemy.com/course/curso-docker

#### DOCKER

    - não é um sistema de virtualização de s.o
    - é um sistema de administração de contêineres que separa um processo de um ambiente
    - host e container compartilham o mesmo kernel
    - empacota software com varios niveis de isolamento
    - o container tem as mesmas caracteristicas de uma vm, porém, com menos consumo de memória
    - xlc x docker
        - o docker abstraiu essa ideia, fazendo com que o container 
          seja um processo mais facil de ser manipulado

#### CONTAINERS

    - modo daemon deixa rodando em background
    - modo iterativo modo de teste
    - arquivos não compartilhados entre containers
    - o run sempre cria um novo container
    - containers devem ter nomes unicos

    - segregação de processos no mesmo kernel (isolamento)
    - sistemas de arquivos criados a partir de uma imagem
    - ambientes leve e portáteis no qual aplicações são executadas
    - encapsula todos os binários e bibliotecas necessárias para executar um programa
    - um container deve ser minimalista, por isso, não deve ter mais de um processo
    - algo entre um chroot e uma vm
        - chroot: aprisiona arquivo em uma pasta
        - vm: ambiente de execução completo
        - docker: isola o processo em um ambiente separado

#### IMAGENS

    - modelo de sistema de arquivos somente-leitura usado para criar um container
    - imagens sao criadas a partir de um processo chamado build
    - são armazenadas em repositorios no registry (docker hub)
    - são compostas por uma ou mais camadas (layers)
    - uma camada representa uma ou mais mudanças no sistema de arquivo (como se fosse um commit)
    - uma camada é também chamada de imagem intermédiaria pois ela 
      possui outros binarios para o binario que voce quer funcionar
      e a junção dessas camadas formam as imagens
    - a apenas a ultima camada pode ser alterada quando o container for iniciado
    - AUFS (advanced multi layered unification filessystem) é muito usado
    - o grande objetivo dessa estrategia de dividir uma imagem em camadas é o reuso
    - é possivel compor imagens a partir de comandos de outras imagens
        - docker.hub

#### IMAGENS VS CONTAINERS

    - docker hub é como o github
    - imagens são classes
    - container são objetos
    - kitematic (versão cliente do CLI do docker)

    - arquitetura
        - daemon vai no registry e faz o download da imagem
        - apos isso faz um cache das imagens
        - caso voce tenha as imagens na maquina ele vai usar as que ja tem
            
#### INSTALAÇÃO

    - linux
        - docker host é o prioprio linux
        - docker daemon é o linux que vai ser o host
        - docker client é o linux que vai ser o cliente

    - mac os
        - o docker host é uma vm linux

    - windows
        - o docker host é uma vm linux no windows
        - quando tem wsl é como se executasse no linux

    - apos o primeiro run a imagem esta em cache

#### CLI CONTAINER

    - o comando run executa quatro comandos
        - docker imagem pull
        - docker container create
        - docker container start
        - docker container exec
        - docker exec -it <nome container> bash

    - docker container run hello-world (container de teste)
    - docker container run debian bash --version  (ver a versão do bash)

    - docker container ps (lista os containers ativos)
    - docker container ps -a (log dos comandos de containers)

    - docker container run --rm debian bash --version (executa e ja remove)
    - docker container run -it debian bash (entra no bash em modo iterativo)
    - docker container run -it --name container-teste debian bash (modo iterativo + nome customizado)

    - docker container ls (lista os containers)
    - docker container ls -a (lista os containers com logs)
    - docker volume ls (lista os volumes)

    - docker container run -p 8080:80 nginx (porta 80 do container para a porta 8080 do host)
    - docker container run -p 8080:80 -v c:/<caminho arquivo>:/usr/share/nginx/html nginx
        -p
            onde 8080 é a porta que o meu pc acessa
            onde 80 é a porta que o container expoe o serviço nginx
        -v
            c:/<caminho arquivo> pasta que eu quero que o nginx veja na minha maquina
            /usr/share/nginx/html pasta do nginx para servir o conteudo
    
    - docker container run -d --name ex-daemon-basic -p 8080:80 -v 
      c:/<caminho arquivo>:/usr/share/nginx/html nginx
        - iniciando o container em modo de background
    
    - docker container start ex-daemon-basic (inicia o container)
    - docker container start -ai ex-daemon-basic (inicia o container em modo iterativo)
    - docker container restart ex-daemon-basic (reinicia o container)
    - docker container stop ex-daemon-basic (para o container)

    - docker container logs ex-daemon-basic (logs do container)
    - docker container inspect ex-daemon-basic (informações do container)
    - docker container exec ex-daemon-basic uname -or (Informações da versão do volume que roda)

    - docker run -dit --name apache_app -p 8080:80 -v 
    c:<caminho arquivo>:/usr/local/apache2/htdocs/ httpd:2.4 (instalando o apache)

    - docker image --help
    - docker container --help
    - docker volume --help

#### CLI IMAGE

    - docker image ls (lista as imagens)
    - docker iamge rm <nome> (remove a imagem)
    - docker image inspect <nome> (informações da imagem)
    - docker image push <nome> (envia a imagem para o registry)
    - docker image pull <nome> (baixa a imagem do registry)
    - docker image tag <imagemorigem> /<imagemdestino> (poe uma tag em uma imagem se baseando em outra)
    - docker image build -t <nome> . (cria uma imagem a partir de um diretorio)

    - docker image tag redis:latest coder-redis (cria uma imagem coder-redis baseada na redis:latest)

    - docker image tag simple-build razielx3/simple-build:1.0

    - docker login --username=<usuario> (faz login no registry)
    - docker image push <nome imagem>:<versao> (envia a imagem para o registry logado)

#### DOCKER IMAGE

    - concatenar layers
    - tentar reaproveitar layers
    - procure manter coisas estaveis na parte de cima do arquivo
    - docker registry: voce pode fazer um registry como um repositorio
    - docker hub: SAAS
    - criar o arquivo Dockerfile com o conteudo das suas imagens

    build simples:
        - docker image build -t <nome> <caminho> (cria uma imagem a partir de um diretorio)
        - docker container run -p 80:80 <nome> (inicia o container mapeando a porta 80 do container para a 80 do host)

    build com argumento
        - pode se passar argumentos para o build assim dando formas de manipular o fluxo
            - docker image build -t arg-build . (cria uma imagem a partir de um diretorio)
            - docker container run arg-build bash -c 'echo $S3_BUCKET' (inicia o container e executa um comando)
            - docker image build --build-arg S3_BUCKET=myapp -t arg-build . (passa um parametro para a variavel do dockerfile)
            - docker container run arg-build bash -c 'echo $S3_BUCKET' (inicia o container e executa um comando)
            - docker image inspect --format '{{index .Config.Env}}' (mostra um dado do inspect)

    - docker container run -p 80:80 copy-build . (inicia o container mapeando a porta 80 do container para a 80 do host)

    - docker image build -t python-build .
    - docker container run -it -v C:\Users\Raziel\Desktop\docker-learning-path\docker\python-build:/app 
      -p 80:8000 --name python-server2 python-build (mapenado o diretorio para dentro do container)
    - docker container run -it --volumes-from=python-server2 debian cat /log/http-server.log

#### DOCKER NETWORK BRIDGE

    - cada container tem a sua rede
    - docker cria uma bridge para abstrair a rede do container e do host
    - tipos de rede
        - none network
        - bridge network (default)
        - host network
        - overlay network (não é muito usado swarm)

    - docker network ls (lista as redes)

    teste de tipos de redes:
        - docker container run -d --net none debian (iniciando rede none)
        - docker container run --rm alpine ash -c "ifconfig"
        - docker container run --rm --net none alpine ash -c "ifconfig"

        - docker container run -d --name container1 alpine sleep 1000 (iniciando rede bridge com nome container1)
        - docker container exec -it container1 ifconfig

        - docker container exec -it container1 ping <ip do outro container> (pinga o outro container)
        - docker network create --driver bridge rede_nova

        - docker container run -d --name container3 --net rede_nova alpine sleep 1000
        - docker container exec -it container3 ifconfig
        - docker network connect bridge container3
        - docker container inspect container1
        - docker network disconnect bridge container3

        - docker container run -d --name container4 --net host alpine sleep 1000

#### DOCKER COMPOSE

    - criar arquivo docker-compose.yml
    - seguir convenção dos containers que baixar
    - com o docker composer override voce consegue sobrescrever valores do arquivo de compose

    - docker-compose up (inicia a composição em modo iterativo)
    - docker-compose up -d (inicia a composição em background)
    - docker-compose exec <container> <comando> (executa comandos dentro do container)
    - docker-compose down (derruba os containers)
    - docker-compose logs -f -t (vigia os logs)
    - docker compose up -d --scale <nome container>=<quantidade> (inicia diversos containers)

    - docker-compose exec db psql -U postgres -c '\l' (executar comando do banco de dados)
    - docker compose exec db psql -U postgres -d email_sender -c 'select * from emails'

<a href="docker\email-build\docker-compose.yml">Primeiro docker composer</a>

- https://medium.com/@FernandoDebrand/criando-um-ambiente-de-desenvolvimento-php-com-docker-compose-a7cad3373df0
- https://dev.to/truthseekers/setup-a-basic-local-php-development-environment-in-docker-kod
- https://github.com/truthseekers/php-docker-simple
- https://towardsdatascience.com/connect-to-mysql-running-in-docker-container-from-a-local-machine-6d996c574e55
- https://stackoverflow.com/questions/33827342/how-to-connect-mysql-workbench-to-running-mysql-inside-docker
