FROM flhosp/apache:centos6
MAINTAINER Kevin Finley <kevishie@gmail.com>

RUN yum --setopt=tsflags=nodocs -y install php && yum clean all

WORKDIR /var/www/html
