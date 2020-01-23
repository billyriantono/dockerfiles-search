#########################################################################
# Base stage
#
FROM ubuntu:bionic AS base-env

# Java and utils
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y openjdk-11-jdk wget gnupg2 imagemagick graphviz iproute2 unzip python curl jq && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# AWS CLI
RUN wget https://s3.amazonaws.com/aws-cli/awscli-bundle.zip
RUN unzip awscli-bundle.zip
RUN ./awscli-bundle/install -b /usr/local/bin/aws

#########################################################################
# Build stage
#
FROM base-env AS build-env

# Comrak
RUN apt-get update && \
    apt-get install -y build-essential curl git
RUN curl https://sh.rustup.rs -sSf | /bin/sh -s -- --default-toolchain stable -y
RUN cd /tmp && \
    git clone https://github.com/kivikakk/comrak.git && \
    cd comrak && \
    $HOME/.cargo/bin/cargo build --release && \
    $HOME/.cargo/bin/cargo install --force

#########################################################################
# Final stage
#
FROM base-env

COPY --from=build-env /root/.cargo/bin/comrak /usr/local/bin/comrak
