FROM centos:7

MAINTAINER Carlos Frias carlos.frias.01@gmail.com

ONBUILD RUN yum update -y 

ONBUILD RUN yum install epel-release -y

RUN yum install -y deltarpm \
    && yum install -y yum-fastestmirror makecache yum-presto \
    && yum makecache fast \
    && yum install -y tar unzip curl wget vim

CMD ["/bin/bash"]
