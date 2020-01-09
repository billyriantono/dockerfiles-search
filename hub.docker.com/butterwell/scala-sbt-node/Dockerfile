# Scala, sbt, and node Dockerfile
#
# https://github.com/butterwell/scala-sbt-node

# Pull base image
FROM hseeberger/scala-sbt:latest

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash
RUN apt-get install --yes nodejs

# Define working directory
WORKDIR /root
