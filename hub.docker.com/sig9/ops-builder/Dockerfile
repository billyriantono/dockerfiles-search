FROM debian:latest

MAINTAINER example@example.com

RUN apt-get update \
 && apt-get -y install build-essential chrpath device-tree-compiler diffstat git libssl-dev openssl python texinfo \
 && cd \
 && git clone https://git.openswitch.net/openswitch/ops-build \
 && cd ops-build \
 && apt-get clean
