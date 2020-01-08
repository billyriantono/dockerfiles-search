FROM selenium/standalone-chrome
ARG DEBIAN_FRONTEND=noninteractive
USER root
RUN echo "nameserver 8.8.8.8" >> /etc/resolv.conf && \
  apt-get update && \
  apt-get install -o Dpkg::Options::=--force-confdef -y  openjdk-8-jdk-headless  && \
  apt-get install -o Dpkg::Options::=--force-confdef -y  maven && \
  rm -rf /var/lib/apt/lists/*
USER seluser
