FROM debian:jessie
MAINTAINER Tikia "renaud@tikia.net"

# Update OS
RUN apt-get update
RUN apt-get -y upgrade

#Define ENV
ENV DEBIAN_FRONTEND noninteractive

#Install ssh-server and others dependencies
RUN apt-get install -y openssh-server wget vim-nox pwgen

#Config OS
RUN mkdir -p /var/run/sshd && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config
RUN sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config
RUN sed -i "s/#PasswordAuthentication/PasswordAuthentication/g" /etc/ssh/sshd_config

#Add password script
ADD https://raw.githubusercontent.com/Tikia/docker-debian/master/root_pw_set.sh /
ADD https://raw.githubusercontent.com/Tikia/docker-debian/master/run.sh /
RUN chmod +x /*.sh

#Define port
EXPOSE 22

#Define CMD
CMD ["/run.sh"]
