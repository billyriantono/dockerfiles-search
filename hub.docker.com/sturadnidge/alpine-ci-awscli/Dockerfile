FROM sturadnidge/alpine-ci:latest
MAINTAINER Stu Radnidge <sturadnidge@gmail.com>
RUN apk add --no-cache \
    python py-pip py-setuptools ca-certificates groff less && \
    pip --no-cache-dir install awscli
