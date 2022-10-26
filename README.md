# docker-lesson
 Introdução ao Docker com o Manual do Dev

Este repositório tem como objetivo estudar Docker com o video do canal do Youtube Manual do Dev

Video: https://youtu.be/01MR38eDXz8

O que foi feito:

1º - Instalação do Docker Desktop

Link: https://www.docker.com/
Link direto Windows: https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=module

Após a instalação foi solicitada a atualização do Kernel do Linux.

A atualização foi realizada utilizando o link indicado pelo Docker, seguindo a partir do quarto passo da documentação em questão até o passo número 5.

Link para a atualização: https://learn.microsoft.com/pt-br/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

Ocorreu ouro erro na inicialização do Docker devido a falta de memória em disco do computador, sendo assim, foi liberado espaço e o Docker foi inicializado corretamente.

2º - Instalação das extensões utilizadas neste aprendizado

Database Client - Para manipular a conexão com o banco de dados
Docker - Para manipular as instâncias do Docker

3º - Download da imagem do MySql e criação do primeiro container

Comando para baixar a imagem e criar o container:

docker run --name mysql_container -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:5.7

Onde:

Execução: docker run
Definir nome do container: --name mysql_container
Variavel de ambiente para o password: -e MYSQL_ROOT_PASSWORD=root
Definição do bind entre a porta do computador e do container: -p 3306:3306 (computador:container)
Rodar em background para manter o terminal acessivel: -d

Após esses passos a imagem ficará visivel na extensão do docker, onde pode ser parada, iniciada, removida, etc.

4º - Conexão ao servidor através do Database Client

Para estabelecer uma conexão é necessário ir até a extensão Database Client e clicar em Create Connection.

Após a abertura da tela de configuração basta preencher os campos necessários para  a conexão funcionar, como o usuário, a senha e a porta.

5º - 


