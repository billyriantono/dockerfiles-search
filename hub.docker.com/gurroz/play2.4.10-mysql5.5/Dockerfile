FROM openjdk:8-jdk

ENV PLAY_VERSION 2.4.10

RUN apt-get update;

# PLAY
RUN curl -O http://downloads.typesafe.com/typesafe-activator/1.3.12/typesafe-activator-1.3.12.zip 
RUN unzip typesafe-activator-1.3.12.zip -d /opt && rm typesafe-activator-1.3.12.zip && chmod a+x /opt/activator-dist-1.3.12/bin/activator
ENV PATH $PATH:/opt/activator-dist-1.3.12/bin/

# MYSQL
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server
RUN sed -i -e "s/^bind-address\s*=\s*\(.*\)/#bind-address = \1/" /etc/mysql/my.cnf
RUN sed -i -e "s/\(\[mysqld\]\)/\1\ncharacter-set-server = utf8/g" /etc/mysql/my.cnf
RUN sed -i -e "s/\(\[client\]\)/\1\ndefault-character-set = utf8/g" /etc/mysql/my.cnf
RUN sed -i -e "s/\(\[mysqldump\]\)/\1\ndefault-character-set = utf8/g" /etc/mysql/my.cnf
RUN sed -i -e "s/\(\[mysql\]\)/\1\ndefault-character-set = utf8/g" /etc/mysql/my.cnf
RUN service mysql start