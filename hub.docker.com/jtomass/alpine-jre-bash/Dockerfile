FROM jetty:jre8-alpine
LABEL maintainer="https://github.com/jtomass/alpine-jre-bash"

USER root
RUN apk add --no-cache \
    bash \ 
    gawk \
    sed \
    grep \
    bc \
    coreutils
USER jetty