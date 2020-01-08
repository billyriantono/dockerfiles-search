FROM alpine:latest

MAINTAINER Dmitrii Demin <mail@demin.co>

RUN apk update \
&&  apk add --update --no-cache mongodb \
&&  echo $'#!/bin/sh\n\
while true; do sleep 60; done\n'\
>> /usr/local/bin/run \
&& chmod +x /usr/local/bin/run

CMD ["/usr/local/bin/run"]
