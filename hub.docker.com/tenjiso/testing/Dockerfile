FROM ubuntu
MAINTAINER Graham Jarvis <gjarvis@tenji-solutions.co.uk>
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd
ONBUILD ADD sshd_config /etc/ssh/sshd_config
USER nobody
WORKDIR /tmp
ENV foobar "Hello World!"
EXPOSE 2222
