FROM alpine:3.7
MAINTAINER Jonas Flodén <jonas@koalasoft.se>

RUN apk --no-cache add python2 py-setuptools

ENV S3_TOOLS_VERSION 2.0.1

RUN wget "http://downloads.sourceforge.net/project/s3tools/s3cmd/${S3_TOOLS_VERSION}/s3cmd-${S3_TOOLS_VERSION}.tar.gz" -q -O - | tar xz -C /tmp && \
    cd /tmp/s3cmd-${S3_TOOLS_VERSION} && \
    python setup.py install && \
    cd / && \
    rm -rf /tmp/s3cmd

ENTRYPOINT ["/usr/bin/s3cmd"]
