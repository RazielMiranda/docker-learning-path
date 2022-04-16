# DOCKER LEARNING PATH

    - NÃO É UM SISTEMA DE VIRTUALIZAÇÃO DE S.O
    - É UM SISTEMA DE ADMINISTRAÇÃO DE CONTÊINERES QUE SEPARA UM PROCESSO DE UM AMBIENTE
    - HOST E CONTAINER COMPARTILHAM O MEMSO KERNEL
    - EMPACOTA SOFTWARE COM VARIOS NIVEIS DE ISOLAMENTO
    - O CONTAINER TEM AS MESMAS CARACTERISTICAS DE UMA VM, PORÉM, COM MENOS CONSUMO DE MEMÓRIA
    - XLC X DOCKER
        - O DOCKER ABSTRAIU ESSA IDEIA, FAZENDO COM QUE O CONTAINER 
          SEJA UM PROCESSO MAIS FACIL DE SER MANIPULADO

#### CONTAINERS

    - SEGREGAÇÃO DE PROCESSOS NO MESMO KERNEL (ISOLAMENTO)
    - SISTEMAS DE ARQUIVOS CRIADOS A PARTIR DE UMA IMAGEM
    - AMBIENTES LEVE E PORTÁTEIS NO QUAL APLICAÇÕES SÃO EXECUTADAS
    - ENCAPSULA TODOS OS BINÁRIOS E BIBLIOTECAS NECESSÁRIAS PARA EXECUTAR UM PROGRAMA
    - UM CONTAINER DEVE SER MINIMALISTA, POR ISSO, NÃO DEVE TER MAIS DE UM PROCESSO
    - ALGO ENTRE UM CHROOT E UMA VM
        - CHROOT: APRISIONA ARQUIVO EM UMA PASTA
        - VM: AMBIENTE DE EXECUÇÃO COMPLETO
        - DOCKER: ISOLA O PROCESSO EM UM AMBIENTE SEPARADO

#### IMAGENS

    - MODELO DE SISTEMA DE ARQUIVOS SOMENTE-LEITURA USADO PARA CRIAR UM CONTAINER
    - IMAGENS SAO CRIADAS A PARTIR DE UM PROCESSO CHAMADO BUILD
    - SÃO ARMAZENADAS EM REPOSITORIOS NO REGISTRY (DOCKER HUB)
    - SÃO COMPOSTAS POR UMA OU MAIS CAMADAS (LAYERS)
    - UMA CAMADA REPRESENTA UMA OU MAIS MUDANÇAS NO SISTEMA DE ARQUIVO (COMO SE FOSSE UM COMMIT)
    - UMA CAMADA É TAMBÉM CHAMADA DE IMAGEM INTERMÉDIARIA POIS ELA 
      POSSUI OUTROS BINARIOS PARA O BINARIO QUE VOCE QUER FUNCIONAR
      E A JUNÇÃO DESSAS CAMADAS FORMAM AS IMAGENS
    - A APENAS A ULTIMA CAMADA PODE SER ALTERADA QUANDO O CONTAINER FOR INICIADO
    - AUFS (ADVANCED MULTI LAYERED UNIFICATION FILESSYSTEM) É MUITO USADO
    - O GRANDE OBJETIVO DESSA ESTRATEGIA DE DIVIDIR UMA IMAGEM EM CAMADAS É O REUSO
    - É POSSIVEL COMPOR IMAGENS A PARTIR DE COMANDOS DE OUTRAS IMAGENS
        - DOCKER.HUB

#### IMAGENS VS CONTAINERS

    - DOCKER HUB É COMO O GITHUB
    - IMAGENS SÃO CLASSES
    - CONTAINER SÃO OBJETOS
    - KITEMATIC

    - ARQUITEURA
        - DAEMON VAI NO REGISTRY E FAZ O DOWNLOAD DA IMAGEM
        - APOS ISSO FAZ UM CACHE DAS IMAGENS
        - CASO VOCE TENHA AS IMAGENS NA MAQUINA ELE  VAI USAR AS QUE JA TEM
            
#### INSTALÇÃO

    - LINUX
        - DOCKER HOST É O PRIOPRIO LINUX
        - DOCKER DAEMON É O LINUX QUE VAI SER O HOST
        - DOCKER CLIENT É O LINUX QUE VAI SER O CLIENTE

    - MAC OS
        - O DOCKER HOST É UMA VM LINUX

    - WINDOWS
        - O DOCKER HOST É UMA VM LINUX NO WINDOWS
        - QUANDO TEM WSL É COMO SE EXECUTASSE NO LINUX

#### HELLO WORLD

    ...