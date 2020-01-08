FROM openjdk:11-jdk-slim

ENV \
  GRADLE_VERSION=4.10.2 \
  GRADLE_HOME=/usr/local/gradle

# GRADLE
RUN \
  cd /usr/local && \
  apt-get update && apt-get install -y wget && \
  wget https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
  unzip gradle-$GRADLE_VERSION-bin.zip && \
  rm -f gradle-$GRADLE_VERSION-bin.zip && \
  ln -s gradle-$GRADLE_VERSION gradle

# AWS CLI
RUN \
  apt-get install -y python-pip && \
  pip install --upgrade awscli

ENV \
  PATH=${PATH}:${GRADLE_HOME}/bin
