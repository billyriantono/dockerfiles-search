FROM frolvlad/alpine-oraclejdk8:8.144.1-slim

LABEL maintainer="Alex Richards <alex@peekvision.org>"

ENV GRADLE_VERSION="4.1"
ENV GRADLE_LOCATION="https://downloads.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip" \
    GRADLE_PATH="/opt/gradle"
ENV GRADLE_HOME="$GRADLE_PATH/current"
ENV PATH="$GRADLE_HOME/bin:$PATH"

WORKDIR $GRADLE_PATH

RUN apk update \
 && apk add wget \
            ca-certificates \
            unzip \
 && update-ca-certificates \
 && wget $GRADLE_LOCATION \
 && unzip gradle-$GRADLE_VERSION-bin.zip \
 && ln -s gradle-$GRADLE_VERSION current \
 && mkdir -p /etc/skel/.gradle \
 && echo "PATH=\"$PATH\"" > /etc/skel/.profile \
 && cp /etc/skel/.profile $HOME \
 && echo -e "org.gradle.daemon=false\nkotlin.compiler.execution.strategy=in-process" > /etc/skel/.gradle/gradle.properties \
 && cp -R /etc/skel/.gradle $HOME
