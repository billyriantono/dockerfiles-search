FROM mysql:latest
MAINTAINER Vikram Chauhan <me@vkrm.ch>

# Override UID and GID
ENV MYSQL_UID=5555
ENV MYSQL_GID=5555

RUN usermod -u $MYSQL_UID mysql \
    && groupmod -g $MYSQL_GID mysql \
    && chown -R mysql:mysql /var/lib/mysql /var/run/mysqld