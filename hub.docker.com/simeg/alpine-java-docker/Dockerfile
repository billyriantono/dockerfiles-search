FROM openjdk:8-jre-alpine
MAINTAINER Simon Egersand <s.egersand@gmail.com>

LABEL org.label-schema.vcs-url="https://github.com/simeg/docker-alpine-java-docker"

RUN apk update && \
    apk add \
	bash \
	docker \
    && \
    sed -i s_#networkaddress.cache.ttl=-1_networkaddress.cache.ttl=60_ $JAVA_HOME/lib/security/java.security && \
    sed -i s_securerandom.source=file:/dev/random_securerandom.source=file:/dev/./urandom_ $JAVA_HOME/lib/security/java.security && \
    rm -rf /var/cache/apk/* && \
    grep ^networkaddress\\\.cache\\\.ttl=60$ $JAVA_HOME/lib/security/java.security && \
    grep ^securerandom\\\.source=file:/dev/\\\./urandom$ $JAVA_HOME/lib/security/java.security
