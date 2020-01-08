FROM maven:3.6-jdk-8-alpine

RUN apk add --no-cache docker

RUN \
    cd /usr/local && \
    curl -L https://services.gradle.org/distributions/gradle-4.4.1-bin.zip -o gradle-4.4.1-bin.zip && \
    unzip gradle-4.4.1-bin.zip && \
    rm gradle-4.4.1-bin.zip

# Export some environment variables
ENV GRADLE_HOME=/usr/local/gradle-4.4.1
ENV PATH=$PATH:$GRADLE_HOME/bin