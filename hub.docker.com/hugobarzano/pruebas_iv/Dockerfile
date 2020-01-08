FROM ubuntu:latest

#Autor
MAINTAINER Hugo Barzano Cruz <hugobarzano@gmail.com>
ENV PYTHONUNBUFFERED 1
#Actualizar Sistema Base
RUN sudo apt-get -y update

#Descargar aplicacion
RUN sudo apt-get install -y git
RUN sudo git clone https://github.com/hugobarzano/pruebas_IV.git

# Instalar Python y PostgreSQL
RUN sudo apt-get install -y python-setuptools
RUN sudo apt-get -y install python-dev
RUN sudo apt-get -y install build-essential
RUN sudo apt-get -y install python-psycopg2
RUN sudo apt-get -y install libpq-dev
RUN sudo easy_install pip
RUN sudo pip install --upgrade pip

#pruebas
#RUN apt-get install -y python-software-properties software-properties-common postgresql-9.3 postgresql-client-9.3 postgresql-contrib-9.3


#Instalamos la aplicacion
RUN ls
RUN cd pruebas_IV/ && ls -l
RUN cd pruebas_IV/ && cat requirements.txt
RUN cd pruebas_IV/ && ls -l
RUN cd pruebas_IV/ && sudo pip install -r requirements.txt

#Realizamos migraciones 

#RUN cat pruebas_IV/ProyectoDjango/settings.py 
#RUN cd pruebas_IV/ && python manage.py syncdb --noinput


