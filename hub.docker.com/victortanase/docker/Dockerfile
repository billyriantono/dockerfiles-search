FROM ubuntu

MAINTAINER Ionel Coste <ic@dsds.com>

RUN apt-get update && apt-get install -y openssh-server

RUN mkdir -p /var/run/sshd

ADD sshd_config /etc/ssh/sshd_config

CMD /usr/sbin/sshd -D

USER root

WORKDIR /tmp
ENV foobar "djjdjsjdsjds"

EXPOSE 2222
CMD ["echo", "Gaga cel viteaz si marul otravit"]
ENTRYPOINT ["echo", "Dockerfile ENTRYPOINT demo\n\n"]
