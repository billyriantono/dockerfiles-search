FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive

ADD provision.sh /provision.sh
RUN chmod +x /provision.sh
RUN ./provision.sh

