# AMB: Dockerfile to create an image with Ant 1.7.0 , jdk 1.6.0,
# 2017/10/16: 0.1 Initial version

FROM openjdk:6b38-jdk-slim

MAINTAINER Agustín Martín Barbero (ambarbero@ree.es)

ENV ANT_VERSION=1.7.0
ENV ANT_HOME=/opt/ant

# change to tmp folder
WORKDIR /tmp

# Install requirements
RUN apt-get update \
        && apt-get install -y --no-install-recommends \
                wget \
        && rm -fr /var/lib/apt/lists/*

# Download and extract apache ant to opt folder
RUN wget --no-check-certificate --no-cookies http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz \
    && wget --no-check-certificate --no-cookies http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz.md5 \
    && echo "$(cat apache-ant-${ANT_VERSION}-bin.tar.gz.md5)  apache-ant-${ANT_VERSION}-bin.tar.gz" | md5sum -c \
    && tar -zvxf apache-ant-${ANT_VERSION}-bin.tar.gz -C /opt/ \
    && ln -s /opt/apache-ant-${ANT_VERSION} /opt/ant \
    && rm -f apache-ant-${ANT_VERSION}-bin.tar.gz \
    && rm -f apache-ant-${ANT_VERSION}-bin.tar.gz.md5

# add executables to path
RUN update-alternatives --install "/usr/bin/ant" "ant" "/opt/ant/bin/ant" 1 && \
    update-alternatives --set "ant" "/opt/ant/bin/ant" 


# Default dir
WORKDIR /source
