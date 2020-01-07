# Basic Ubuntu base installation

FROM ubuntu:14.04
MAINTAINER Patrick Merlot <patrick.merlot@gmail.com>

USER root
ENV DEBIAN_FRONTEND noninteractive

# Install the basic packages
RUN apt-get update
RUN apt-get install -y wget rsync build-essential emacs git ca-certificates
