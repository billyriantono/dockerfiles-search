FROM alpine:3.9.4

ARG VERSION=8

RUN apk update --no-cache && \
    apk add openjdk${VERSION}-jre curl && \
    rm -rf /tmp /var/cache

ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk/

ENTRYPOINT ["java"]
CMD ["-version"]
