FROM centos:7

MAINTAINER Rafael Pinho <rafaelpinho@protonmail.com>

COPY ./mongodb-enterprise.repo /etc/yum.repos.d/

RUN yum install -y mongodb-enterprise && \
    mkdir -p /data/db && \
    rm -dfr /var/cache \
            /usr/share/man \
            /usr/include \
            /etc/ssl \
            /tmp/*

CMD mongod
