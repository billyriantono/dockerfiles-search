FROM centos:latest

MAINTAINER niuyuxian "ncc0706@gmail.com"

#Install sshd net-tools
RUN yum install -y openssh-server net-tools

RUN mkdir /var/run/sshd

#set password for root
RUN echo 'root:node' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

#set history record
ENV HISTTIMEFORMAT "%F %T  "

#Fix sshd service:Read from socket failed: Connection reset by peer?
RUN ssh-keygen -A

#Open 22 port
EXPOSE 22

#Auto running sshd service
CMD ["/usr/sbin/sshd","-D"]
