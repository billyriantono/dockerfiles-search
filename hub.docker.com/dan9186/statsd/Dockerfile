FROM centos

MAINTAINER Daniel Hess <dan9186@gmail.com>

RUN yum install -y epel-release && \
    yum update -y && \
    yum upgrade -y && \
    yum install -y git tar nodejs && \
    yum clean all

WORKDIR /opt
RUN git clone git://github.com/etsy/statsd.git

WORKDIR /
ADD docker-entrypoint.sh docker-entrypoint.sh

EXPOSE 8125/udp

ENTRYPOINT ["/docker-entrypoint.sh"]
