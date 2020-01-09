FROM ubuntu:16.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode

# Update the repository sources list
#RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y sudo

RUN apt-get install -y mysql-server

RUN apt-get install -y bc

EXPOSE 3306

RUN chown -R mysql:mysql /var/lib/mysql
RUN echo "mysql ALL = NOPASSWD: /usr/sbin/service mysql start" | cat >> /etc/sudoers
RUN echo "nobody ALL = NOPASSWD: /usr/sbin/service mysql start" | cat >> /etc/sudoers


ADD sql_runner.sh /compilebox/
ADD create_user.sql /compilebox/
ADD destroy_user.sql /compilebox/
ADD file.sql /compilebox/usercode/

#RUN sed -i 's/\/var\/run\/mysqld\/mysqld.sock/\/run\/mysqld\/mysqld.sock/g' /etc/mysql/my.cnf
#ENTRYPOINT service mysql start && /bin/bas

RUN sudo chmod -R 777 /var/lib/mysql
#CMD service mysql start
#RUN sudo chown -R nobody /var/lib/mysql