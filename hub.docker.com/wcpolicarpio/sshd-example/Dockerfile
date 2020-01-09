FROM ubuntu

MAINTAINER Walter Policarpio at Morgan Solar Inc.<wcpolicarpio@gmail.com>

RUN apt-get update && apt-get install -y openssh-server

RUN mkdir -p /var/run/sshd

ONBUILD ADD sshd_config /etc/ssh/sshd_config
CMD /usr/sbin/sshd -D


USER nobody 
WORKDIR /tmp
ENV FOO "bar"


EXPOSE 2222
