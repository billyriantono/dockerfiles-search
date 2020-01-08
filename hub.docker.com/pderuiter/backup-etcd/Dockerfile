FROM alpine

MAINTAINER De Ruiter IT Consultancy <dockerimages@bsdserver.nl>

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories 
RUN apk update --no-cache && \
    apk add --no-cache curl && \
    apk add --no-cache aws-cli && \
    apk add --no-cache etcd && \
    apk add --no-cache etcd-ctl && \
    apk add --no-cache bash && \
    apk add --no-cache dos2unix

ADD VERSION .
COPY backup-etcd.sh /
RUN ["chmod", "+x", "/backup-etcd.sh"]
RUN dos2unix /backup-etcd.sh
RUN apk del dos2unix
CMD ["/backup-etcd.sh"]
