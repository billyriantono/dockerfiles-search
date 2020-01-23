FROM centos:centos7
MAINTAINER Mehul Bhatt <mehulsbhatt@hotmail.com> <https://mehulbhatt.com> <@mehulbhatt>
RUN yum -y update
RUN yum -y install epel-release
RUN yum -y install mongodb-server
RUN yum -y clean all
RUN mkdir -p /data/db
EXPOSE 27017
ENTRYPOINT ["/usr/bin/mongod"]
