FROM openjdk:8-alpine
MAINTAINER amaya <mail@sapphire.in.net>

WORKDIR /app/

RUN wget http://central.maven.org/maven2/it/unimi/dsi/webgraph/3.5.2/webgraph-3.5.2.jar && \
  wget http://webgraph.di.unimi.it/webgraph-deps.tar.gz && \
  tar xzf webgraph-deps.tar.gz && rm webgraph-deps.tar.gz
