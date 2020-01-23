FROM openjdk:8-jdk-alpine

ARG GENERATOR_VERSION=4.1.3

RUN wget http://central.maven.org/maven2/org/openapitools/openapi-generator-cli/${GENERATOR_VERSION}/openapi-generator-cli-${GENERATOR_VERSION}.jar -O /openapi-generator-cli.jar

VOLUME /local

WORKDIR /local

CMD ["java", "-jar", "/openapi-generator-cli.jar"]
