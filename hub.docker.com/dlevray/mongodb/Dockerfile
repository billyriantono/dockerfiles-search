FROM dlevray/basestack
MAINTAINER David LEVRAY <dlevray@gmail.com>
LABEL version="1.0"
LABEL description="MongoDB database configured for OpenStack" 
LABEL readme="this image is used for installing the Openstack telemetry component"

RUN yum install -y epel-release.noarch  && \
  yum update -y && \
  yum install -y mongodb-server mongodb && \
  yum clean all && \
  systemctl enable mongod.service

COPY mongodb /etc/mongod.conf 

EXPOSE 27017

CMD ["/usr/sbin/init"]
