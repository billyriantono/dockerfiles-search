FROM alpine:3.1
MAINTAINER Jose Monreal <jmonreal@gmail.com>

WORKDIR /tmp

COPY inc/tmp/install.sh /tmp/
COPY inc/tmp/test.sh /tmp/
RUN sh /tmp/install.sh
RUN sh /tmp/test.sh
RUN rm -f /tmp/{install,test}.sh

WORKDIR /

ENTRYPOINT ["/bin/etcd"]

CMD []

