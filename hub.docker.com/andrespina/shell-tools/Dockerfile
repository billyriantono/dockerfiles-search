FROM debian:stretch-slim

RUN apt-get update && \
  apt-get install openssl -y

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*