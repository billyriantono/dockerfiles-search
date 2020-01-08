FROM centos:centos7
MAINTAINER Yohan Graterol <y@platzi.com>

EXPOSE 22

RUN yum -y update
RUN yum clean all
RUN yum -y install openssh-server passwd
RUN yum clean all
COPY start.sh /start.sh
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N ''

RUN chmod 755 /start.sh

ENTRYPOINT ["/start.sh"]
CMD ["/usr/bin/sshd", "-D"]
