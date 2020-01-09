FROM multiarch/alpine:aarch64-edge
MAINTAINER "zikloa <mengliu@me.com>"
ADD requirements.txt .
RUN apk add --update python python-dev gcc libgcc libc-dev py2-pip libev openssl-dev && \
    pip install -r requirements.txt && \
    apk del python-dev gcc libgcc libc-dev py2-pip libev openssl-dev && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*
ADD dockerdns .
EXPOSE 53
ENTRYPOINT ["./dockerdns"]
