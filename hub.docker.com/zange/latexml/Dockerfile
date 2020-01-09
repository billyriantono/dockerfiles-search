FROM debian:jessie

MAINTAINER Marian Zange <marian.zange@tum.de>

RUN apt-get update && apt-get install -y latexml
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*