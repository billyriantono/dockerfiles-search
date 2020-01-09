FROM debian:jessie
MAINTAINER Benjamin Böhmke

# Install Latex
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install git texlive-full curl && \
    rm -rf /var/lib/apt/lists/*

# set working directory
WORKDIR /data
VOLUME /data