# Only client.
FROM ubuntu:14.04

MAINTAINER marcie001 <marcie00001@gmail.com>

RUN apt-get install -y mysql-client-5.5
ADD my.cnf /etc/mysql/my.cnf

VOLUME ["/work"]
