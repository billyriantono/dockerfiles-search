FROM openjdk:11-jre-slim

RUN apt-get update && \
    apt-get install -y openssl curl

ONBUILD ARG BUILD_VERSION_NO="no-version"

ENV SPRING_PROFILES_ACTIVE=pro

ONBUILD COPY $TARGET_DIR/*.jar app.jar
ONBUILD RUN sh -c 'touch /app.jar'
ONBUILD RUN echo "$BUILD_VERSION_NO" > /version

EXPOSE 8080

ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -jar /app.jar" ]