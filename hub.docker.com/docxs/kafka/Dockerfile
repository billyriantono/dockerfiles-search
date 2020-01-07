########################################################################
# Dockerfile for Kafka
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Component:    Kafka
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-kafka
# License:      MIT
########################################################################

# pull base image
FROM \
  docxs/java:8

# maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# Set environment variables
ENV KAFKA_SCALA_VERSION 2.11
ENV KAFKA_VERSION_MAJOR 0
ENV KAFKA_VERSION_MINOR 8
ENV KAFKA_VERSION_BUILD 2
ENV KAFKA_VERSION_PATCH 1
ENV KAFKA_VERSION ${KAFKA_VERSION_MAJOR}.${KAFKA_VERSION_MINOR}.${KAFKA_VERSION_BUILD}.${KAFKA_VERSION_PATCH}
ENV KAFKA_HOME /opt/kafka

# Install kafka
RUN curl -jksSL http://apache.mirrors.pair.com/kafka/${KAFKA_VERSION}/kafka_${KAFKA_SCALA_VERSION}-${KAFKA_VERSION}.tgz | tar -xzf - -C /opt \
 && ln -s /opt/kafka_${KAFKA_SCALA_VERSION}-${KAFKA_VERSION} ${KAFKA_HOME}

# Set additional environment variables
ENV PATH $PATH:$KAFKA_HOME/bin

# Add configuration files
ADD config /src/config

# Add the binary files
ADD bin /bin/

# expose the relevant ports
EXPOSE \
  9092 7203

# Run bootstrap on container launch
ENTRYPOINT \
  ["bootstrap"]

# Default command runs kafka server
CMD \
  ["-server"]
