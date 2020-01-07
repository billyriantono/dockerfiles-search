FROM ubuntu:14.04
MAINTAINER Tiago Rolim <tiago.rol@gmail.com>

#Non interactive
ENV DEBIAN_FRONTEND noninteractive

#Atualizando o Linux
RUN sudo apt-get update && \
    sudo apt-get -y upgrade

#Instalando o nginx
RUN sudo apt-get -y install nginx

#Configutrando o nginx
RUN sudo service nginx start && \
    sudo update-rc.d nginx defaults && \
    sudo service nginx restart

ADD nginx.conf /etc/nginx/

#Permissão
ADD run.sh /usr/local/bin/run.sh
RUN sudo chmod +x /usr/local/bin/run.sh

EXPOSE 80

CMD ["/usr/local/bin/run.sh"]
