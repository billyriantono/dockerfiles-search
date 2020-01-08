FROM centos:6.4
MAINTAINER "Huan Zhang" <huan_zh@yahoo.com>

RUN yum -y update
RUN yum -y install openssh-server supervisor 

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''
RUN echo "root:redhat" | chpasswd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
