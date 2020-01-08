FROM centos:7
MAINTAINER daicham <daicham@gmail.com>

RUN yum update -y && yum install epel-release -y
RUN yum install -y ansible openssh-clients

CMD ["ansible", "--version"]
