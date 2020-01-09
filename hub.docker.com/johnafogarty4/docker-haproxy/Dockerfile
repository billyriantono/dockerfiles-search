# HAProxy
#
# Version 0.0.1

FROM centos:7.1.1503

ENTRYPOINT ["/usr/sbin/haproxy", "-f", "/haproxy.cfg", "-d"]

EXPOSE 3306

ADD haproxy.cfg /haproxy.cfg

RUN /bin/localedef -v -c -i en_US -f UTF-8 en_US.UTF-8;\
    yum -y install haproxy; \
