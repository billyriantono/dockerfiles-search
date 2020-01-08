FROM centos:centos7
MAINTAINER Mehul Bhatt <mehulsbhatt@hotmail.com> <https://mehulbhatt.com> <@mehulbhatt>
RUN yum -y update
RUN yum -y install epel-release
RUN yum -y install redis
RUN yum -y clean all
EXPOSE 6379
CMD [ "redis-server" ]
