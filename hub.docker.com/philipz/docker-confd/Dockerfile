FROM busybox:latest
MAINTAINER Philipz <philipzheng@gmail.com>

ADD ./confd /bin/
RUN chmod +x /bin/confd

RUN mkdir -p /etc/confd/conf.d
RUN mkdir -p /etc/confd/templates

VOLUME ["/etc/confd","/tmp"]
CMD ["/bin/confd"]
