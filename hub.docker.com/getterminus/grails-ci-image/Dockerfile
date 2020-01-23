FROM openjdk:7u211-jdk-alpine3.9

# Java reads the timezone name from /etc/timezone and uses that to look up
# timezone data in its own db. We're also updating /etc/localtime to be
# consistent because other programs use it.
RUN apk --no-cache --update add tzdata && \
    ln -s /usr/share/zoneinfo/UTC /etc/localtime && \
    echo "UTC" > /etc/timezone

ENV GRAILS_VERSION 2.2.1

WORKDIR /usr/lib
RUN apk --no-cache --update --virtual .install-deps add wget && \
    wget -q https://github.com/grails/grails-core/releases/download/v${GRAILS_VERSION}/grails-${GRAILS_VERSION}.zip && \
    apk --no-cache del .install-deps && \
    unzip -q grails-${GRAILS_VERSION}.zip && \
    rm -rf grails-${GRAILS_VERSION}.zip && \
    ln -s grails-${GRAILS_VERSION} grails

ENV GRAILS_HOME /usr/lib/grails
ENV PATH ${GRAILS_HOME}/bin:${PATH}

WORKDIR /
