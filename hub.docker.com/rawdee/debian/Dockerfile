FROM debian:wheezy
MAINTAINER Rodolphe Blancho

# configure Apt to use less disk space
ADD etc /etc

ENV LC_ALL C.UTF-8
RUN echo 'LC_ALL=C.UTF-8' >> /etc/environment
ENV DEBIAN_FRONTEND noninteractive
RUN echo 'DEBIAN_FRONTEND=noninteractive' >> /etc/environment

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y localepurge curl \
  && apt-get autoremove -y \
  && apt-get clean -y \
  && localepurge

