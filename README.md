# Docker: Utilização prática no cenário de Microsserviços

Este é um exemplo de como um microsserviço pode ser acessado através de um IP, e executar uma rotina específica, como inserção em um banco de dados.


Os containers para habilitar os serviços de banco de dados e servidor web foram criados com os comandos abaixo no Docker:

* MySQL
```
docker run --name mysql-A -d -p 3306:3306 --mount type=bind,src=/home/vboxuser/Desktop/docker/data/desafio-1/mysql-A/,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD=Senha123 mysql:5.7
```
* Apache
```
docker run --name web-server -dt -p 80:80 --mount type=bind,src=/home/vboxuser/Desktop/docker/data/desafio-1/,dst=/app/ webdevops/php-apache:alpine-php7
```

Com o MySQL Workbench foram utilizados os comandos SQL abaixo para criação do banco de dados e da tabela de exemplo:

* Criação do banco de dados
```
create database meubanco
use meubanco
```
* Criação da tabela de exemplo
```
CREATE TABLE dados (
	AlunoID int,
    Nome varchar(50),
    Sobrenome varchar(50),
    Endereco  varchar(150),
    Cidade varchar(50),
    Host varchar(50)
)
```

A pasta desafio-1 contém um arquivo index.php, que foi acoplada ao container Apache com o parâmetro --mount.
Quando o serviço é acionado pelo ip local, através do browser na porta 80, o código php é executado e inclui um registro aleatório no banco de dados.

Caso o host que hospeda estes serviços estiver com IP público na Internet, é possível utilizar ferramentas de testes como loader.io, que fará requisições sucessivas ao serviço web, incluindo assim, vários registros no banco de dados.
