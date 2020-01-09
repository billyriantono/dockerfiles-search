# from https://github.com/openzipkin/docker-zipkin/tree/master/zipkin
# from https://bitbucket.org/wholerendevteam/docker-zipkin
FROM nerelohw/docker-openjdk:8-jre-alpine3.7
MAINTAINER OpenZipkin "http://zipkin.io/"

ENV ZIPKIN_REPO https://jcenter.bintray.com
ENV ZIPKIN_VERSION 2.9.0

# Use to set heap, trust store or other system properties.
ENV JAVA_OPTS -Djava.security.egd=file:/dev/./urandom

# Add environment settings for supported storage types
COPY rootfs/_zipkin/ /zipkin/
RUN chmod a+x /zipkin/mysql/init.sh
WORKDIR /zipkin

RUN apk add unzip curl --no-cache && \
    curl -SL $ZIPKIN_REPO/io/zipkin/java/zipkin-server/$ZIPKIN_VERSION/zipkin-server-$ZIPKIN_VERSION-exec.jar > zipkin-server.jar && \
    # don't break when unzip finds an extra header https://github.com/openzipkin/zipkin/issues/1932
    unzip zipkin-server.jar ; \
    rm zipkin-server.jar && \
    curl -SL $ZIPKIN_REPO/io/zipkin/java/zipkin-autoconfigure-collector-scribe/$ZIPKIN_VERSION/zipkin-autoconfigure-collector-scribe-$ZIPKIN_VERSION-module.jar > scribe.jar && \
    unzip scribe.jar -d scribe && \
    rm scribe.jar && \
    curl -SL $ZIPKIN_REPO/io/zipkin/java/zipkin-autoconfigure-collector-kafka10/$ZIPKIN_VERSION/zipkin-autoconfigure-collector-kafka10-$ZIPKIN_VERSION-module.jar > kafka10.jar && \
    unzip kafka10.jar -d kafka10 && \
    rm kafka10.jar && \
    apk del unzip


EXPOSE 9410 9411

CMD test -n "$STORAGE_TYPE" && source /zipkin/profiles/${STORAGE_TYPE}_profile;\
    test -n "$STORAGE_TYPE" && [ "$STORAGE_TYPE" == "mysql" ] && bash -c /zipkin/mysql/init.sh; \
    test -n "$SCRIBE_ENABLED" && JAVA_OPTS="${JAVA_OPTS} -Dloader.path=scribe -Dspring.profiles.active=scribe"; \
    test -n "$KAFKA_BOOTSTRAP_SERVERS" && JAVA_OPTS="${JAVA_OPTS} -Dloader.path=kafka10 -Dspring.profiles.active=kafka"; \
    exec java ${JAVA_OPTS} -cp . org.springframework.boot.loader.PropertiesLauncher
