FROM alpine:3.10.3

MAINTAINER Nemo <dockerfile@captnemo.in>
ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Tinyproxy" \
      org.label-schema.vcs-url="https://github.com/captn3m0/docker-tinyproxy.git" \
      org.label-schema.url="https://github.com/captn3m0/docker-tinyproxy" \
      org.label-schema.vcs-ref=$VCS_REF

RUN apk add --no-cache tinyproxy dumb-init

COPY default.conf /etc/tinyproxy/tinyproxy.conf

COPY init /init

ENTRYPOINT ["/init"]
