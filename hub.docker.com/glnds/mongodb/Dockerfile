FROM centos:centos7
MAINTAINER Gert Leenders <leenders.gert@gmail.com>

# Add the latest MongoDB release repository (3.0)
ADD mongodb-org-3.0.repo /etc/yum.repos.d/

RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install mongodb-org; yum clean all
# Use the line below to link a specific MongoDB version
# RUN yum install -y mongodb-org-3.0.6 mongodb-org-server-3.0.6 mongodb-org-shell-3.0.6 mongodb-org-mongos-3.0.6 mongodb-org-tools-3.0.6; yum clean all
RUN mkdir -p /data/db

EXPOSE 27017
ENTRYPOINT ["/usr/bin/mongod"]
