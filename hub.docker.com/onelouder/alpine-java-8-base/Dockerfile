FROM alpine:3.5

ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
    echo '#!/bin/sh'; \
    echo 'set -e'; \
    echo; \
    echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
  } > /usr/local/bin/docker-java-home \
  && chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u111
ENV JAVA_ALPINE_VERSION 8.121.13-r0

ENV JAVA_OPTS="-Xms256m -Xmx1024m -XX:PermSize=1024m -XX:MaxPermSize=1024m"

RUN set -x \
  && apk add --no-cache \
    openjdk8="$JAVA_ALPINE_VERSION" \
  && [ "$JAVA_HOME" = "$(docker-java-home)" ]

# add bash and coreutils curl jq
RUN apk add --update --no-cache \
    bash \
    coreutils \
    curl \
    jq \
    tcpdump \
    ca-certificates \
    && \
    update-ca-certificates \
    && \
    rm -rf /var/cache/apk/*

# We added a VOLUME pointing to "/tmp" because that is where a Spring Boot application creates working directories for
# Tomcat by default. The effect is to create a temporary file on your host under "/var/lib/docker" and link it to the
# container under "/tmp". This step is optional for the simple app that we wrote here, but can be necessary for other
# Spring Boot applications if they need to actually write in the filesystem.

VOLUME /tmp

# Wired Docker healthcheck to Springboot Actuator for Health Check
#HEALTHCHECK --interval=90s --timeout=90s --retries=6 CMD curl --fail http://localhost:8080/admin/health || exit 1

########
## Install envconsul, consul-template, and tini
## envconsul will import config items from consul and vault as environment variables
## consult-template injects consul and vault properties into templates
## tini will init our containers, whether that's witn envconsul, consul-template or just a CMD
########
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && apk add --no-cache envconsul consul-template tini \
 && sed -i '/http:\/\/dl-cdn.alpinelinux.org\/alpine\/edge\/testing/d' /etc/apk/repositories

COPY *.sh /app/
COPY templates/* /app/templates/
RUN chmod 750 /app/*.sh

ENTRYPOINT ["/sbin/tini", "--", "/app/entrypoint.sh"]
