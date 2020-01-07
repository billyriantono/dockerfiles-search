FROM centos:7

RUN yum -y update && yum -y install squid
RUN ln -sf /dev/stdout /var/log/squid/cache.log

COPY squid.conf /etc/squid/squid.conf

ENTRYPOINT ["/usr/sbin/squid"]
CMD ["-N"]
