# ${registry}/java:oracle-8u101-jdk-alpine
#
# The main caveat to note is that it does use musl libc instead of glibc and friends,
# so certain software might run into issues depending on the depth of their libc requirements.
# However, most software doesn't have an issue with this,
# so this variant is usually a very safe choice.
#
FROM alpine:3.3
MAINTAINER haolunzhang@yirendai.com

# Smaller Java images with Alpine Linux
# see: https://developer.atlassian.com/blog/2015/08/minimal-java-docker-containers/

# Install cURL
# https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk
# https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk
# http://o9wbz99tz.bkt.clouddn.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk
# see: http://wiki.alpinelinux.org/wiki/Setting_the_timezone
RUN apk --update add bash git openssh curl ca-certificates tar tzdata && \
    curl -Ls http://o9wbz99tz.bkt.clouddn.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk > /tmp/glibc-2.23-r3.apk && \
    apk add --allow-untrusted /tmp/glibc-2.23-r3.apk && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apk del tzdata

ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
# 设置时区 中国的时区有多种表述 分别为: UTC+8:00 GMT+8
ENV TZ GMT-8
ENV JAVA_OPTS -Duser.language=zh -Duser.region=CN -Dfile.encoding='UTF-8' -Duser.timezone='Asia/Shanghai'

ADD docker/install_jdk.sh /root/
RUN /root/install_jdk.sh

# Set environment
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
