FROM composer

RUN apk update
RUN apk add rsync openssh

RUN addgroup -S jenkins -g 1000 && adduser -S jenkins -G jenkins -u 1000
