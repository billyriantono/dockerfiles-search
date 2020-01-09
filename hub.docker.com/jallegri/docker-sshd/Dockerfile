FROM ubuntu:14.04

MAINTAINER Wei-Ming Wu <wnameless@gmail.com>

RUN apt-get update

# Install sshd
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

# Set password to 'admin'
RUN printf admin\\nadmin\\n | passwd

EXPOSE 22

CMD /usr/sbin/sshd -D
