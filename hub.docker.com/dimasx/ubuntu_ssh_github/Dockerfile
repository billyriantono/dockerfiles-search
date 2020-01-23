#---------------------------------------------------------------------------
# Dockefile to build Docker Image of OpenSSH-Server running on Ubuntu
#
# Made by Dmitry Lobachev  19-Dec-2019
#---------------------------------------------------------------------------

FROM ubuntu:latest

RUN apt-get -y update && \
	       apt-get install -y net-tools && \ 
	       apt-get install -y iputils-ping && \
	       apt-get install -y curl && \
               apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:mypasswdroot' |chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN mkdir /root/.ssh
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]

