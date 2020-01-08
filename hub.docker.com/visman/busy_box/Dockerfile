FROM centos:7.3.1611

RUN yum update -y && \
    yum install -y epel-release && \
    yum install -y mc git gnupg screen && \
    yum clean all

#set local data and sync time
RUN rm -rf /etc/localtime && \
    ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime

ADD .screenrc /root/.screenrc
