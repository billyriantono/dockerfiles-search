FROM debian:jessie
LABEL maintainer="aj@garcialagar.es"
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y apt-transport-https ca-certificates
RUN apt-get upgrade -y && rm -rf /var/lib/apt/lists/*
RUN useradd -m -s /bin/bash user
