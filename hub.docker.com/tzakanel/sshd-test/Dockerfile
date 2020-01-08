FROM ubuntu

MAINTAINER Alex Stevens <tzakanel@yahoo.com>

RUN apt-get update && apt-get install openssh-server -y && mkdir -p /var/run/sshd

ADD sshd_config /etc/ssh/sshd_config

CMD /usr/sbin/sshd -D

USER nobody

WORKDIR /tmp

EXPOSE 2222
