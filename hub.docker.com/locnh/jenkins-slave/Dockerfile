FROM centos:7

MAINTAINER Loc Nguyen <me@locnh.com>

COPY slave.jar /opt/slave.jar
COPY kick-start.sh /opt/kick-start

RUN chmod -v +x /opt/kick-start

# Install packages
RUN yum -y install java git && yum clean all

CMD ["/opt/kick-start"]
