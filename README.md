# Introdução ao Docker com o Manual do Dev

Este repositório tem como objetivo estudar **Docker** com o video do canal do **Youtube** **Manual do Dev**

Video: <https://youtu.be/01MR38eDXz8>


## O que foi feito:

### 1º - Instalação do Docker Desktop

Link: <https://www.docker.com/>
</br>
Link direto Windows: <https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=module>

Após a instalação foi solicitada a atualização do *Kernel do Linux*.

A atualização foi realizada utilizando o link indicado pelo *Docker*, seguindo a partir do quarto passo da documentação em questão até o passo número 5.

Link para a atualização: <https://learn.microsoft.com/pt-br/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package>

>Ocorreu um erro na inicialização do Docker devido a falta de memória em disco do computador, sendo assim, foi liberado espaço e o *Docker* foi inicializado corretamente.

### 2º - Instalação das extensões utilizadas neste aprendizado

**Database Client** - Para manipular a conexão com o banco de dados.
</br>
**Docker** - Para manipular as instâncias do Docker.

### 3º - Download da imagem do MySql e criação do primeiro container

Comando para baixar a imagem e criar o container:

~~~cmd
docker run --name mysql_container -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:5.7
~~~


Onde:

- **Execução:** docker run
- **Definir nome do container:** --name mysql_container
- **Variavel de ambiente para o password:** -e MYSQL_ROOT_PASSWORD=root
- **Definição do bind entre a porta do computador e do container:** -p 3306:3306 (computador:container)
- **Rodar em background para manter o terminal acessivel:** -d

Após esses passos a imagem ficará visivel na extensão do docker, onde pode ser parada, iniciada, removida, etc.

### 4º - Conexão ao servidor através do Database Client

Para estabelecer uma conexão é necessário ir até a extensão *Database Client* e clicar em *Create Connection*.

Após a abertura da tela de configuração basta preencher os campos necessários para  a conexão funcionar, como o usuário, a senha e a porta.

Para conectar é necessário clicar em *Connect*.

### 5º - Criando uma base de dados

Para criar uma base de dados basta clicar em *New Database* no explorer do *Database Client* intitulado com o ip da conexão.
Um código *SQL* será gerado automaticamente para a criação da base, sendo necessário apenas preencher o nome da base e clicar em *Executar*.

### 6º - Criando uma imagem de um projeto

A criação de uma imagem de um projeto é utilizada para transportar um ambiente de desenvolvimento de uma aplicação para outra máquina, para que outros desenvolvedores possam contribuir com o mesmo projeto, sem a necessidade de uma reconfiguração da sua própria máquina para que ela aceite o novo app.

Primeiro é criado um arquivo com o nome *Dockerfile* sem nenhuma extensão na raiz do projeto, com as seguintes linhas:

~~~dockerfile
// Imagem do node que irá utilizar para construir a imagem base
FROM node:16-alpine

// Diretório de trabalho (pasta escolhida para salvar o projeto dentro do container)
WORKDIR /app

// Cópia dos pacotes de configuração do projeto
COPY package*.json /app/

// Linha de comando para instalar as dependências do Node
RUN npm install

// Cópia de todos os arquivos do projeto para a pasta app
COPY . /app/

// Exposição da porta do container (3000:React)
EXPOSE 3000

// Comando para iniciar a aplicação
CMD [ "npm", "start" ]

~~~

Para construir a imagem a partir deste arquivo criado é necessário executar os seguintes comandos:

~~~cmd
// -t - Nome da imagem
// . - Raíz do projeto
docker build -t meu_app .
~~~

### 7º - Rodar o container criado

~~~cmd
// -p - Porta que foi utilizada no arquivo de configuração do app
docker run --name react_app -p 3000:3000 meu_app
~~~
