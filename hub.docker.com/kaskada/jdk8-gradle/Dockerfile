FROM java:8-jdk

ENV GRADLE_VERSION 2.5

RUN apt-get update && apt-get install -y docker.io

RUN wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip && \
    unzip gradle-${GRADLE_VERSION}-all.zip && \
    ln -s /gradle-${GRADLE_VERSION}/bin/gradle /usr/bin/gradle
