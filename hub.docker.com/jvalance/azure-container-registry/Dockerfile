#
# Ubuntu with Java and Maven

# pull base image
FROM ubuntu:latest
LABEL Jeremy Valance "jvalance@blackducksoftware.com"

RUN \
  apt-get update && \
  apt-get install -y openjdk-8-jdk && \
  apt-get install -y maven && \
  apt-get install -y git && \
  rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Change working directory
WORKDIR /app

# run maven and pull down detect
RUN \
  git clone https://github.com/valancej/duck-hub.git && \
  cd duck-hub && \
  mvn package