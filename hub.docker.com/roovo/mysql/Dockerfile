FROM roovo/ubuntu:12.04

MAINTAINER roovo "roovo@roovoweb.com"

RUN apt-get -y install mysql-server-5.5
RUN apt-get clean

RUN sed -i -e "s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf

ADD ./startup /opt/startup

EXPOSE 3306

CMD ["/bin/bash", "/opt/startup"]
