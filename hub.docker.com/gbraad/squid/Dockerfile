FROM centos:7
MAINTAINER Gerard Braad <me@gbraad.nl>

RUN yum -y install squid && \
    yum clean all && \
    systemctl enable squid

COPY squid.conf /etc/squid/

VOLUME /etc/squid

EXPOSE 3128/tcp

CMD [ "/sbin/init" ]
