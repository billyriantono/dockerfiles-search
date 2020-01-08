#
# Copyright (c) 2001-2018 Primeton Technologies, Ltd.
# All rights reserved.
#
# author: ZhongWen Li (mailto:lizw@primeton.com)
#

FROM primetoninc/jdk:1.6

# LABEL maintainer="lizw@primeton.com" \
#     provider="Primeton Technologies, Ltd."

# build environment settings
ENV MAVEN_HOME=/opt/apache-maven-3.2.5

ENV PATH="${PATH}:${MAVEN_HOME}/bin"

RUN curl --fail --location --retry 3 \
        https://archive.apache.org/dist/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz \
        -o /tmp/maven.tar.gz \
    && tar -zvxf /tmp/maven.tar.gz -C /opt/ \
    && \rm -f /tmp/maven.tar.gz
