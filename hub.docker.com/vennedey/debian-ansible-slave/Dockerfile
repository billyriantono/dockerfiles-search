FROM debian:jessie
MAINTAINER Falco Vennedey "docker@vennedey.net"

ENV SSHPORT 22
ENV PUBLICKEY ""
EXPOSE $SSHPORT

RUN apt-get update &&  apt-get install --no-install-recommends --no-install-suggests -y \
	openssh-server \
	python2.7 \
	python

COPY files/etc/ssh/sshd_config /etc/ssh/sshd_config
RUN echo "Port $SSHPORT" >> /etc/ssh/sshd_config

RUN mkdir -p /root/.ssh /var/run/sshd
COPY files/usr/local/sbin/init.sh /usr/local/sbin/init.sh
RUN chmod 700 /usr/local/sbin/init.sh

CMD /usr/local/sbin/init.sh
