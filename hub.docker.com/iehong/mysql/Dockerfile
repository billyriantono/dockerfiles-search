FROM ubuntu:14.04

RUN sudo apt-get update \
    && sudo apt-get install -y mysql-server \
    && apt-get clean \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV ROOTPWD='123456'

EXPOSE 3306
VOLUME /var/lib/mysql
COPY ./my.conf /etc/mysql/my.conf
COPY dockermysql /usr/local/bin/
RUN chmod 777 /usr/local/bin/dockermysql \
    && chmod 700 /var/lib/mysql \
    && chown -R mysql:mysql /var/lib/mysql
ENTRYPOINT dockermysql