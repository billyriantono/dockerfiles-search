########################################################################
# Dockerfile for Cassandra
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
# Component:    Cassandra
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-cassandra
# License:      MIT
########################################################################

# Pull base image
FROM \
  docxs/java:8

# Maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# Set environment variables
ENV CASSANDRA_VERSION_MAJOR 2
ENV CASSANDRA_VERSION_MINOR 2
ENV CASSANDRA_VERSION_BUILD 4
ENV CASSANDRA_VERSION ${CASSANDRA_VERSION_MAJOR}.${CASSANDRA_VERSION_MINOR}.${CASSANDRA_VERSION_BUILD}
ENV CASSANDRA_HOME /opt/cassandra

# Install cassandra
RUN apt-prepare \
 && apt-get install -q -y \
      python \
 && curl http://www.eu.apache.org/dist/cassandra/${CASSANDRA_VERSION}/apache-cassandra-${CASSANDRA_VERSION}-bin.tar.gz | tar -xzf - -C /opt \
 && ln -s /opt/apache-cassandra-${CASSANDRA_VERSION} $CASSANDRA_HOME \
 && apt-cleanup

# Set additional environment variables
ENV PATH $PATH:$CASSANDRA_HOME/bin

# Add configuration files
ADD config /src/config

# Add the binary files
ADD bin /bin/

# expose the relevant ports
EXPOSE \
  7000 7001 7199 9042 9160 61621

# Run bootstrap on container launch
ENTRYPOINT \
  ["bootstrap"]

# Default command
CMD \
  ["-cassandra"]
