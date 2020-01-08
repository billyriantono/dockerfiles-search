FROM centos:7

RUN yum -y update
RUN yum -y reinstall glibc-common
RUN yum -y install tar
RUN yum -y clean all

CMD /usr/bin/bash
