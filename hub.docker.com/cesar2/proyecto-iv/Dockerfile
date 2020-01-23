FROM ubuntu:latest

#Autor
MAINTAINER Cesar Albusac Jorge <cesypozo@gmail.com>

#Actualizar Sistema Base
RUN sudo apt-get -y update

#Descargar aplicacion 
RUN sudo apt-get install -y git
RUN sudo git clone https://github.com/cesar2/Proyecto-IV.git

#Instalar Python y PostgreSQL
RUN sudo apt-get install -y python-setuptools
RUN sudo apt-get -y install python-dev
RUN sudo apt-get -y install build-essential
RUN sudo apt-get -y install python-psycopg2
RUN sudo apt-get -y install libpq-dev
RUN sudo easy_install pip
RUN sudo pip install --upgrade pip

#Instalar la app
RUN cd Proyecto-IV && make install
