FROM centos:7
MAINTAINER Koji Saiki <saikou9901@gmail.com>

RUN yum install -y openssh-clients
RUN yum install -y expect

COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

CMD ["/sbin/entrypoint.sh"]