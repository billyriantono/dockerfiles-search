# https://hub.docker.com/_/maven/
# Take a maven slim image with jdk8 to build jar
FROM maven:3.6.1-jdk-8-alpine AS maven

# Declaring variables
ENV JAR_FILE target/wochat-code-manager-service*.jar
ENV CODE_SOURCE /opt/service

# Setting up working directory
RUN mkdir -p ${CODE_SOURCE}
ADD . ${CODE_SOURCE}
WORKDIR ${CODE_SOURCE}

# Compiling / Packaging the jar
RUN mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -B -V
RUN cp ${JAR_FILE} application.jar

# Switch to dind image
FROM docker:18.09.6-dind

# Install Java-8
RUN apk update && apk add --no-cache openjdk8

# Declaring variables
ENV CODE_SOURCE /opt/service

# Set up working directory
RUN mkdir -p ${CODE_SOURCE}
WORKDIR ${CODE_SOURCE}

# Copy jar file from "maven" image
COPY --from=maven ${CODE_SOURCE}/application.jar ./application.jar

# Run Code
ENTRYPOINT java -jar application.jar

