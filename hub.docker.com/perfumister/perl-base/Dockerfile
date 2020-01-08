# Ubuntu 16.04 LTS with Perl 5.22.1, App::cpanminus & Carton

FROM ubuntu:xenial
MAINTAINER Perfumister <hey@perfumister.com>

# Update and install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -y \
        apt-utils build-essential locales git curl \
        perl cpanminus carton
RUN locale-gen en_US.UTF-8 && \
    dpkg-reconfigure locales

# Clean up!
RUN apt-get autoclean
