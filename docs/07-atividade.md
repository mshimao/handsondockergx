# Atividade 07

## Docker Compose

### Implantação de uma aplicação Genexus com Docker Compose

Nesta atividade tente criar uma infra estrutura para executar uma aplicação .Net Core acessando um servidor SQL Server com o banco de dados num Volume Docker.

![Infra Docker Compose](imagens/infra-dockercompose.png)

#### Passo 1

No Genexus, 

![target dir](imagens/targetenvdir.png)

Crie na pasta C:\HandsOnDocker um arquivo com o nome "docker-compose-gx-sql.yml" e digite o conteúdo abaixo.

```docker-compose
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8888:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```

Inicialmente crie um volume para persistir os dados do MySQL e configure um contêiner para usar esse volume seguindo as instruções do post (Criando Volumes com Docker)[https://blog.alura.com.br/criando-volumes-com-docker/].

Use a imagem do MySQL que já foi baixada na atividade anterior para subir o contêiner:

```bash
mysql:5.7
```
Também será necessário configurar a senha do root informando o valor da variável MYSQL_ROOT_PASSWORD no parâmetro -e (variáveis de ambientes do contêiner).

``` bash
-e MYSQL_ROOT_PASSWORD=password 
```

Depois que o contêiner estiver ativo, conecte com o HeidiSQL para verificar se o MySQL está funcionando adequadamente.

Agora crie um environment novo no Genexus com .NET Core e MySQL.

![Genexus env](imagens/genexus-env.png)

Execute o create da base de dados e depois execute a aplicação para verificar que a aplicação está gravando os dados.

Agora que a aplicação está rodando, faça o deploy da aplicação para o Docker.

Depois da imagem criada edite o aquivo docker-compose.yml para refletir a infraestrutura desejada, com a aplicação GX, o servidor MySQL e o volume.

- [Documentação do Docker Compose - volumes](https://docs.docker.com/compose/compose-file/#volumes)

Um ponto importante é a configuração da conexão da aplicação com o banco de dados, o Genexus tem o recurso de configurar a aplicação através de variáveis de ambiente. Veja no link abaixo como fazer isso e coloque as configurações necessárias no docker compose file.

- [Application Configuration using Environment Variables](https://wiki.genexus.com/commwiki/servlet/wiki?39459,Application+Configuration+using+Environment+Variables)

Com o arquivo docker-compose.yml editado, execute o comando `docker-compose up` e veja se a aplicação executa corretamente.