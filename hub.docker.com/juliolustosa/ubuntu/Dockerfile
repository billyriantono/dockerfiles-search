FROM ubuntu:16.04
MAINTAINER Julio Lustosa "contato@juliolustosa.com.br"

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    apt-transport-https \
    ca-certificates \
    build-essential \
    tzdata \
    git-core \
    cron \
    curl \
    software-properties-common \
    python-software-properties

# Install packages with recommends
RUN apt-get install -y \
    upstart \
    monit

# Upgrade all packages.
RUN apt-get upgrade -y -o Dpkg::Options::="--force-confold"

# Copy scripts
RUN mkdir -p ./build-scripts
COPY ./build-scripts /build-scripts
RUN chmod +x /build-scripts/*.sh

# Install
RUN /build-scripts/install.sh