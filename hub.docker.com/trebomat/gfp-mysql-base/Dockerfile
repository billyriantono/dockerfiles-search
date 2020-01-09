# Base image to tag trebomat/gfp-mysql-base
FROM mysql:5.7.23
MAINTAINER Mathieu Obert <trebomat@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

ADD custom.cnf /etc/mysql/conf.d/custom.cnf
ADD config.sql /docker-entrypoint-initdb.d/config.sql

RUN chmod -R +x /docker-entrypoint-initdb.d
