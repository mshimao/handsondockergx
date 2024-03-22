# Atividade 07

## Docker Hub

O Docker Hub é um repositório público de imagens de containers, onde diversas empresas e pessoas podem publicar imagens pré-compiladas de soluções. Essas soluções incluem desde WordPress, MySql e outras aplicações diversas.
Nele, você encontra imagens prontas para uso, criadas por desenvolvedores da comunidade, projetos open-source e fornecedores de software independentes (ISVs).

### Publicando uma imagem no Docker Hub

#### Passo 1

Abra um prompt de linha de comando e digite o comando `docker login`. Informe o usuário e senha que foi criado anteriormente.

![docker login](imagens/dockerhublogin.png)

#### Passo 2

Acesse o site do Docker Hub e faça login.

- [Docker Hub](https://hub.docker.com/)

#### Passo 3

Na aba "Repositories", pegue o nome da conta, no exemplo da imagem é "mkshimao".

![Docker Hub Web](imagens/dockerhubweb.png)

#### Passo 4

No Genexus, editar as opções de deploy, clicando em "options". 
Acrescentar o nome da conta do Docker Hub no campo "Docker Image name", neste exemplo o nome da imagem ficaria "mkshimao/handsondockernetsqlserver"

![GX Docker Image Name](imagens/deployoptions.png)

#### Passo 5

Clicar no botão "Deploy" para gerar a imagem com o novo nome.

![GX build Image](imagens/deploybuildimage2.png)

#### Passo 6

Na linha de comando, executar o comando `docker images` para conferir se a imagem foi criada.

![Docker images](imagens/dockerlistimage2.png)

Notar que a imagem foi gerada com a TAG latest, poderia ter ser o número da versão, como no caso do mysql que tem a tag "8.0".

#### Passo 7

Na linha de comando, executar o comando `docker push docker_id/nome_do_repositorio:TAG` para publicar a imagem, substituindo docker_id pelo nome da conta, nome_do_repositorio pelo nome da imagem e TAG por latest. No exemplo do handson o comando ficaria assim: `docker push mkshimao/handsondockernetsqlserver:latest`.

![Docker push](imagens/dockerpush.png)

#### Passo 8

Acesse o site do Docker Hub, na aba repositories, verifique se a imagem aparece na lista.

![Docker Hub Images](imagens/dockerhubimages.png)

Lembrando que essa imagem foi publicada na área pública e que está disponível para qualquer um acessar. Para projetos de clientes o ideal é publicar as imagens na área privada ou publicar num serviço de repositório privado, como do Azure.

## Documentação do Docker Hub

Para maiores detalhes sobre o Docker Hub, consultar a documentação abaixo:

- [Documentação do Docker Hub](https://docs.docker.com/docker-hub/)

