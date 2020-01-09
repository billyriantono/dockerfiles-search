FROM ubuntu:16.04
#Owned by who now?
MAINTAINER MinTh<bom19985@gmail.com>

#update ubuntu
RUN apt-get update -y

#install nginx
RUN apt-get install nginx apt-utils -y

#install mysql
RUN echo "mysql-server mysql-server/root_password password root" | debconf-set-selections \
    && echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections \
    && apt-get install -y mysql-server

WORKDIR /venv

COPY start.sh /venv

RUN chmod a+x /venv/*

ENTRYPOINT ["/venv/start.sh"]

EXPOSE 80 
