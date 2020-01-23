FROM openjdk:jdk-slim as builder

RUN mkdir -p /build/
WORKDIR /build/

COPY . /build/

# Should fix StackOverflow errors
ARG MAVEN_OPTS="-Xms256m -Xmx1024m -Xss1024k"

# Install maven
RUN apt-get update &&  \
    apt-get install -y maven git

# Builds the launcher
RUN mvn package && \
    mv target/vnflauncher-1.0-SNAPSHOT-jar-with-dependencies.jar /vnflauncher.jar


FROM java:8
ENV PORT=8080
ENV LINKS=http://localhost
WORKDIR /
COPY --from=builder /vnflauncher.jar /vnflauncher.jar
EXPOSE $PORT
CMD java -jar vnflauncher.jar $PORT $LINKS
