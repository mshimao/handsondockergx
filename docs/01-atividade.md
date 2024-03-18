# Atividade 01

## hello-world

Neste primeiro exercicio vamos fazer o conhecido hello-world. Para isso abra um tela de linha comando e execute o comando `docker run hello-world`.

```bash
C:\> docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:41a65640635299bab090f783209c1e3a3f11934cf7756b09cb2f1e02147c6ed8
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

Ao executar esse comando, o Docker irá verificar que se a imagem existe no nosso computador, não existindo a imagem, ele executa o download da imagem do Docker Hub e inicia o contêiner.

Se executarmos o comando [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) serão listados os contêineres.

```bash
C:\>docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS           NAMES
```

Veja que não existe nenhum contêiner rodando, vamos executar uma variação do comando ps e ver o que acontece. Execute o comando `docker ps -a`.

```bash
c:\>docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
30567b2dd8d4        hello-world         "/hello"            About an hour ago   Exited (0) About an hour ago                       trusting_jackson
```

Na lista apareceu o contêiner que foi executado e agora está parado.

Próximo: [Atividade 02](02-atividade.md)