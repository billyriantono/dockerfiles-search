FROM centos:latest

ENV TOKEN=none

RUN yum -y update && \
    yum -y install bind-utils && \
    yum -y install postgresql \ 
    yum -y install telnet \
    yum -y install httpie
RUN set -o vi

CMD [ "/bin/sleep", "3600" ]
