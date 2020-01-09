FROM ubuntu:14.04

MAINTAINER Mario Zieschang <mziescha@cpan.org>

RUN    apt-get update -y && apt-get upgrade -y \
    && apt-get install -y make gcc vim openssl libssl-dev git \
    && apt-get autoremove -y \
    && apt-get clean \
    && cpan -i Menlo \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*