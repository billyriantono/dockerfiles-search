FROM centos:centos6.6

MAINTAINER CloudRunner.IO Dev, dev@cloudrunner.io

RUN yum -y install epel-release
RUN yum update -y
RUN yum -y install python-zmq python-pip m2crypto python-msgpack python-psutil

RUN mkdir -p /etc/cloudrunner
RUN mkdir -p /opt/cloudrunner
RUN mkdir -p /var/run/sock/cloudrunner/
RUN mkdir -p /var/lib/cloudrunner/

RUN pip install cloudrunner
RUN cloudrunner-node configure --server 0.0.0.0
RUN cloudrunner-node details

ADD startup /opt/startup
ADD cloudrunner-node.conf /etc/cloudrunner/cloudrunner-node.conf

ENTRYPOINT ["/opt/startup"]
