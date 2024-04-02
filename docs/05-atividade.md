# Atividade 04

## Persistência de dados

Quando um contêiner é desligado, os dados gravados no contêiner são perdidos, então como não perder as informações? Para isso existem 2 alternativas, utilizar Volume ou Bind mount.

## Docker Volume

Volumes no Docker são mecanismos preferenciais para persistir dados gerados e utilizados por containers Docker. Enquanto os bind mounts dependem da estrutura de diretórios e do sistema operacional da máquina hospedeira, os volumes são completamente gerenciados pelo Docker. Aqui estão algumas características importantes dos volumes:

- Persistência e Gerenciamento:
    - Os volumes são mais fáceis de fazer backup ou migrar do que os bind mounts.
    - Você pode gerenciar volumes usando comandos da CLI Docker ou a API Docker.
    - Funcionam tanto em containers Linux quanto em Windows.
    - Podem ser compartilhados com segurança entre vários containers.
- Drivers de Volume:
    - Os drivers de volume permitem armazenar volumes em hosts remotos ou provedores de nuvem, criptografar o conteúdo dos volumes ou adicionar outras funcionalidades.
    - Novos volumes podem ter seu conteúdo pré-populado por um container.
- Desempenho:
    - Os volumes no Docker Desktop têm desempenho muito superior aos bind mounts de hosts Mac e Windows.

## Bind mount

No Docker, um bind mount é um mecanismo que permite montar um diretório ou arquivo do sistema de arquivos do host dentro de um container Docker. Vamos explorar os detalhes:
- Funcionamento:
    - Com um bind mount, um diretório ou arquivo específico no host é montado no container.
    - O caminho absoluto desse diretório ou arquivo no host é usado como referência.
    - Ao contrário dos volumes, que são gerenciados pelo Docker, os bind mounts dependem da estrutura de diretórios do sistema de arquivos do host.
- Diferenças entre Volumes e Bind Mounts:
    - Volumes criam um novo diretório dentro do armazenamento do Docker no host.
    - Bind mounts usam diretamente o caminho do host.

### Acessando uma pasta do Host usando bind mount

#### Passo 1

Vamos executar o comando `docker run -v c:/HandsOnDocker:/data alpine ls /data`, o parâmetro `-v` mapea a pasta C:\HandsOnDocker do Windows para a pasta /data do Linux Alpine, está sendo passado o comando `ls` para listar os arquivos da pasta data.

![docker volume](imagens/dockervolume.png)

Vemos que o Docker mapeou a pasta corretamente e mostrou o conteúdo.

#### Passo 2

Agora vamos executar criar o contêiner usando o parâmetro `-it` para podermos executar comandos no bash do Linux. Após o contêiner subir execute o comando ls para listar as pastas.

```bash
docker run -it -v c:/HandsOnDocker:/data alpine
```

![linux ls](imagens/linuxls.png)

#### Passo 3

Execute o comando `cd data` para entrar na pasta data. Agora vamos criar uma aquivo texto usando a instrução `cat > teste.txt`. Digite alguma coisa, dê enter e depois aperte CTRL + D para sair do arquivo. Execute o comando `ls` para listar os arquivos.

![linux cat](imagens/linuxcatfile.png)

Verifique se na pasta C:\HandsOnDocker do Windows aparece o arquivo teste.txt.

![windows files](imagens/windowsfiles.png)

### Criando um volume

#### Passo 4

Agora vamos trabalhar com volumes, vamos criar um volume usando o comando `docker volume create` com o nome de "dados".

```bash
C:\HandsOnDocker>docker volume create dados
dados

C:\HandsOnDocker>docker volume ls
DRIVER              VOLUME NAME
local               dados
```

#### Passo 5

Crie agora um contêiner usando esse volume, para isso use o parâmetro `-v dados:/var/dados`, esse parâmetro mapea o volume dados para a pasta /var/dados do contêiner.

```bash
C:\HandsOnDocker>docker run -it --name servidor -v dados:/var/dados alpine
/ # cd var
/var # ls
cache  dados  empty  lib    local  lock   log    opt    run    spool  tmp
/var #
```
#### Passo 6

Agora vá até a pasta /var/dados e crie uma arquivo texto chamado teste.txt usando o comando `cat > teste.txt` e CRTL + D para sair do arquivo.

```bash
/var/dados # ls
teste.txt
```

#### Passo 7

Abra outra tela de linha de comando, vamos criar um outro contêiner usando o volume dados, dando um nome diferente do anterior. Verifique se o arquivo criado anteriormente está lá.

```bash
C:\HandsOnDocker>docker run -it --name servidor2 -v dados:/var/dados alpine
```

#### Passo 8

Crie um outro arquivo na pasta dados e vá para a tela do contêiner anterior e liste o conteúdo da pasta, você verá que o arquivo criado aparece, ou seja os dois contêineres estão compartilhando o mesmo volume. 

```bash
/var/dados # ls
teste.txt   teste2.txt
/var/dados #
```
Agora conseguimos persistir informações mesmo que o contêiner pare ou seja apagado, podemos usar o volume para armazenar as bases de dados de um servidor de banco de dados ou outros dados relevantes.

## Documentação do Docker Volume

Para maiores detalhes sobre o Docker Volume, consultar a documentação abaixo:

- [Documentação do Docker Volume](https://docs.docker.com/storage/volumes/)

Próximo: [Atividade 06](06-atividade.md)