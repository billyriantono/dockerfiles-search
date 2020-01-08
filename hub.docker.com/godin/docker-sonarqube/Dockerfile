FROM alpine:3.7

RUN apk add --no-cache gnupg \
    && ping -c 5 ha.pool.sks-keyservers.net \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && gpg --keyserver pgp.mit.edu --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
