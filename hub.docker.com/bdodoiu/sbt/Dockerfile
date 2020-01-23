#
# sbt Dockerfile
#
# https://github.com/bdodoiu/sbt
#

# Pull base image
FROM openjdk:8

# Env variables
ENV SBT_VERSION 1.2.1

# Install sbt
RUN \
  curl -L -o sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt && \
  sbt sbtVersion

# Define working directory
WORKDIR /root