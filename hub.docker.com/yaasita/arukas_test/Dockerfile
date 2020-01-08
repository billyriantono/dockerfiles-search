FROM debian:stretch
MAINTAINER yaasita

#apt
RUN apt-get update
RUN apt-get upgrade -y

#package
RUN apt-get install -y vim git \
 aptitude openssh-server

RUN mkdir /var/run/sshd/
RUN mkdir /root/.ssh
ADD authorized_keys /root/.ssh/authorized_keys
RUN perl -i -ple 's/^(permitrootlogin\s)(.*)/\1yes/i' /etc/ssh/sshd_config
EXPOSE 22
CMD /usr/sbin/sshd -D
