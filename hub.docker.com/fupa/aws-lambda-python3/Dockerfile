FROM fupa/alpine-aws:latest

MAINTAINER Johannes "Sepp" Stadler <j.stadler@fupa.net>

# update packages
RUN apk update  --progress && \
    apk upgrade --progress

RUN mkdir /var/task
WORKDIR /var/task
ENV WORKDIR /var/task

# node is required for serverless
RUN apk add nodejs npm --progress

