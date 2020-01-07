FROM alpine:3.10
MAINTAINER Demiurg (parserpro@gmail.com)

RUN apk update && apk add perl perl-dev curl tar make gcc build-base && rm -fr /var/cache/apk/*

RUN cd /bin && curl -L https://cpanmin.us/ -o cpanm && chmod +x cpanm

RUN cpanm --no-wget -n App::cpm
