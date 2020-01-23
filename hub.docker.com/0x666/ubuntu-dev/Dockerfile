FROM       ubuntu:latest
MAINTAINER Marcus Przybilla "https://github.com/mprzybilla/docker-ubuntu-dev"

ENV SSH_PORT 22
ENV ROOT_PWD root

RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo 'root:${ROOT_PWD}' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir /root/.ssh

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get update && \
    apt-get -y upgrade

EXPOSE ${SSH_PORT}

CMD    ["/usr/sbin/sshd", "-D"]