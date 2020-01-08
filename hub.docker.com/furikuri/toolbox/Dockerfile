FROM alpine:3.6
MAINTAINER Theo Pack <tf.pack@gmail.com>

RUN apk add --update curl bind-tools tcpdump python3 && \
    pip3 install --upgrade pip setuptools httpie && \
    rm -rf /var/cache/apk/*

CMD ["/bin/sh"]