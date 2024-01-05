# 1. Docker na prática
Projeto de uma aplicação web simples em python/flask com mysql deployed by docker

O projeto segue as aulas da playlist de docker na Prática com Python

# 2. Docker 

## 2.1 Startar o docker

```bash
sudo service docker start
```

## 2.2 Usar docker sem sudo

Antes de tudo, deve-se criar um grupo chamado `docker`
```bash
sudo groupadd docker
```

Agora, basta adicionar o seu usuário ao grupo `docker`:
```bash
sudo usermod -aG docker USER
```

Após utilizar o comando, basta sair da sessão e logar novamente.

## 2.3 Imagens

ver as imagens instaladas

``` bash
sudo docker images
```

Criar uma imagem de um dockerfile
``` bash
docker build . --tag docker-python
```

## 2.4 Remover container
remover container 
``` bash
sudo docker rm [CONTAINER ID]
```

remover container que esta rodando
``` bash
sudo docker rm [CONTAINER ID] --force
```
## 2.5 Criar um container de uma imagem
``` bash
sudo docker run [image]
```

Criar container mais completo com alguns parametros
```bash
docker run -e MYSQL_ROOT_PASSWORD=[senha_secreta] -p 3306:3306 --name mysqldb --network mynet -v mysqlVolume:/var/lib/mysql -d mysql:latest
```

## 2.6 Rodar um container ja criado

``` bash
sudo docker start [CONTAINER ID]
```

Iniciar todos os containers
``` bash
sudo service docker start
```

## 2.7 Ver os containers

ver os containers que estão executando
``` bash
sudo docker ps 
```
ver os containers ativos e inativos
``` bash
sudo docker ps -a
```

## 2.8 Entrar no CLI do container

``` bash
sudo docker exec -it [CONTAINER ID] bash
```

## 2.9 Parar containers

``` bash
sudo docker stop [CONTAINER ID]
```

Fechar todos os container
```bash
sudo service docker stop
```

## 2.10 Ver as configurações do container que esta inicializado

```bash
docker inspect [CONTAINER ID]
```

## 2.11 Criar container com endereço de IP pareado e detached 

```bash
docker run -p 2300:5000 -d docker-python
```

## 2.12  solving mysql connection problem
url de conection no dbeaver
```url 
jdbc:mysql://localhost:3306/?allowPublicKeyRetrieval=true&useSSL=false
```

https://otty.hashnode.dev/using-docker-to-run-mysql-on-wsl2
Connection to mysql - ip adress

- from wsl2 terminal:
```bash
localhost:3306
```

- from windows host
```bash
ip a show eth0
```
or
```bash
ip a
```

## 2.13 Volumes

https://docs.docker.com/storage/

Ver volumes
```bash
docker volume ls
```

Deletar volumes
```bash
docker volume rm [volume_name]
```
## 2.14 Criar um db e uma tabela no mysql

Criar arquivo schema.sql
```sql
CREATE DATABASE IF NOT EXISTS teste;
CREATE TABLE IF NOT EXISTS `teste`.`users` (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Digitar no cli:
```bash
docker exec -i [CONTAINER_ID] mysql -u root -pmysql <./schema.sql
```

## 2.15 Entrar na linha de comando - cli - bash do container

```bash
docker exec -i [CONATAINER_ID] bash
```

## 2.16 network (rede)

Ver as redes do docker
```bash
docker network ls
```

Criar uma network
```bash
docker network create [nome_da_rede]
```

Remover network
```bash
docker network rm [NETWORK_ID]
```

## 2.17 Executar um comando no mysql no docker

```bash
mysql -u root -p -e "SHOW DATABASES;"
```

## 2.18 Rodando uma imagem de python buildada com conexão com mysql alguns parâmetros
```bash
docker run -p 3000:5000 --network mynet docker-pythonv2
```

# 3. Docker Compose
## 3.1 Geral

https://docs.docker.com/language/python/develop/

## 3.2 Executando docker compose
```bash
docker compose up --build
```

# 4. Arquivos utilizados para configuração do Docker

.dockerignore

compose.yaml

Dockerfile

schemas.sql


