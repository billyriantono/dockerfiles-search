FROM centos:7.6.1810

RUN set -x && \
    yum -y update && \
    yum -y install \
    epel-release

RUN set -x && \
    yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

RUN set -x && \
    yum -y install \
    awscli \
    docker-ce \
    findutils \
    git \
    hostname \
    make \
    docker-compose
