FROM ubuntu:12.04
MAINTAINER Apasfot Formacion "norbertocb@msn.com"

##Actualizamos el sistema
RUN apt-get update
##Instalamos nginx
RUN apt-get install -y nginx

#RUN echo 'Mi primer Dockerfile' > /usr/share/nginx/www/index.html

##VOLUME
VOLUME /usr/share/nginx/wwww/

##ARG##
ARG webpage
ADD $webpage/ /usr/share/nginx/www

##Arrancamos NGINX a través de Entrypoint para que no pueda ser modificado en la creación del contenedor
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

#Exponer el puerto 80
EXPOSE 80
