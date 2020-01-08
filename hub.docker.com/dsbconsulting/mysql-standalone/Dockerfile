FROM dsbconsulting/ubuntu:14.04

RUN apt-get update \
 && apt-get install -y mysql-server \
 && rm -rf /var/lib/mysql/mysql \
 && rm -rf /var/lib/apt/lists/*

ENV DB_REMOTE_ROOT_PASS secret
ADD start /start
RUN chmod 755 /start

EXPOSE 3306
ENV DB_REMOTE_ROOT_NAME root
ENV DB_REMOTE_ROOT_PASS secret

VOLUME ["/var/lib/mysql"]
VOLUME ["/run/mysqld"]

CMD ["/start"]
