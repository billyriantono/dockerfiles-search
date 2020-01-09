FROM openjdk:8-jdk-alpine

ARG CLI_VERSION=3.0.0-rc1

RUN wget http://central.maven.org/maven2/io/swagger/swagger-codegen-cli/${CLI_VERSION}/swagger-codegen-cli-${CLI_VERSION}.jar -O /swagger-codegen-cli.jar

VOLUME /local

WORKDIR /local

CMD ["java", "-jar", "/swagger-codegen-cli.jar"]
