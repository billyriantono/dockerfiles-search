### Dockerfile
#
#   See https://github.com/reconnix/docker

FROM reconnix/base:CentOS6
MAINTAINER Russ McKendrick <russ.mckendrick@reconnix.com>
RUN yum -y install http://dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
RUN yum -y install python-pip mysql mysql-server
RUN echo "NETWORKING=yes" > /etc/sysconfig/network
RUN pip install "pip>=1.4,<1.5" --upgrade
RUN pip install supervisor
ADD supervisord.conf /etc/
ADD run /usr/local/bin/
RUN chmod +x /usr/local/bin/run
CMD ["/usr/local/bin/run"]