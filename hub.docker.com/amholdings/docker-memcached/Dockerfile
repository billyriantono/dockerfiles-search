FROM centos:centos7
MAINTAINER Mehul Bhatt <mehulsbhatt@hotmail.com> <https://mehulbhatt.com> <@mehulbhatt>
RUN yum -y update && yum clean all && yum install -y epel-release
RUN yum install -y memcached
# Port to expose
EXPOSE 11211
# run
CMD /usr/bin/memcached -p 11211 -u memcached -m 64 -c 1024
