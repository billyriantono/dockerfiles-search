########################################################################
# Dockerfile for Mongodb
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
# Component:    Mongodb
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/docxs/docker-mongodb
# License:      MIT
########################################################################

# Pull base image
FROM \
  docxs/base:latest

# Maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# Define a mountable data directory
VOLUME \
  ["/data"]

# Set environment variables
ENV MONGODB_VERSION_MAJOR 3
ENV MONGODB_VERSION_MINOR 0
ENV MONGODB_VERSION_BUILD 4
ENV MONGODB_VERSION ${MONGODB_VERSION_MAJOR}.${MONGODB_VERSION_MINOR}.${MONGODB_VERSION_BUILD}

# Install mongodb
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10 \
 && echo "deb http://repo.mongodb.org/apt/debian wheezy/mongodb-org/${MONGODB_VERSION_MAJOR}.${MONGODB_VERSION_MINOR} main" > /etc/apt/sources.list.d/mongodb-org.list \
 && apt-prepare \
 && apt-get install -q -y \
      adduser mongodb-org=${MONGODB_VERSION} \
 && apt-cleanup

# Add configuration files
ADD config /src/config

# Add the binary files
ADD bin /bin/

# expose the relevant ports
EXPOSE \
  27017 28017

# Run bootstrap on container launch
ENTRYPOINT \
  ["bootstrap"]

# Default command
CMD \
  ["-mongod"]
