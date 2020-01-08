FROM ubuntu:14.04
ENV SSH_PW SecretPassword303
ENV SSH_KEY ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDc33eMyvfsXcsHYtCcVuLj3NEBI2JK8rYNRmh3B2p+ka/uFERfy6eXLiOULLEUdse93sir1ycUp+gfoL2WuR3o/GaPXcAXQlKnG/n2jAbtEOS7Zz85sLcndBp4SynA7QQXwMo0Vvb4CVII7sA2hxCiP5FslUvZU3E3jXDPhaYD8dpZUBObY4oOpWLNXutumwHASPJ8sa4QcCHII4hw4HyFOjYw2iUViYNhUeYQykHlfzgANeoiJQWEzKWwa+RtUP94I9r9qRtfQl5k5YsA7rcX2mvQcgEWMknemx3Prw6uSSVwEt9WuNmWoa73xxtbxeBefu+TB5pZprgt+QwbysKl jenkins
RUN apt-get update -qq && apt-get install -y openssh-server openjdk-7-jdk git apt-transport-https && \
    echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 && \
    apt-get update -qq && \
    apt-get install -qqy lxc-docker && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir /var/run/sshd

RUN useradd -s /bin/bash -m -d /work jenkins
ADD ./startup.sh /startup.sh
EXPOSE 22
ENTRYPOINT ["/startup.sh"]
