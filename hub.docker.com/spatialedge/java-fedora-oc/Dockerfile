# Pull base image. We start from Ubuntu because it has docker.io available by default.
FROM fedora:29

# Env variables
ENV JAVA_VERSION 1.8.0

RUN \
  dnf -y install java-${JAVA_VERSION}-openjdk-devel origin-clients docker maven

# Define working directory
WORKDIR /root