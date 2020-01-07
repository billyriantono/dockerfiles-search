from vishnu667/alpinebase:latest

MAINTAINER Vishnu Prasad <vishnu667@gmail.com>

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="e.g. https://github.com/vishnu667/dockerImages" \
      org.label-schema.vcs-ref=$VCS_REF

RUN apk add --update ruby libffi-dev ruby-dev ruby-io-console zlib-dev ruby-irb  ruby-rdoc

Run rm -rf /var/cache/apk/*
WORKDIR /root
