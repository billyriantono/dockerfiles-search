FROM frolvlad/alpine-glibc:alpine-3.6

#
# 2016-2017 © Headcount Solutions Ltd.
# See 'LICENCE.md' in the project root for more information.
#

MAINTAINER Neil Hyland <neil.hyland@bimandscan.com>

# Install Java runtime & cleanup package cache:
RUN apk update && \
    apk add --no-cache openjdk8-jre \
                       bash && \
    rm -rf "/var/cache/apk/*"

ENV JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk/" \
    PATH=${PATH}:"/usr/lib/jvm/java-1.8-openjdk/bin"
