FROM centos:7

USER       root
RUN        yum install -y wget curl telnet bind-utils iproute\
           && yum clean all
USER       nobody
WORKDIR    /tmp
ENTRYPOINT ["tail", "-f", "/dev/null"]