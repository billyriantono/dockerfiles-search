FROM ubuntu:14.04

RUN \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get \
        -o Dpkg::Options::="--force-confnew" \
        --force-yes \
        -fuy dist-upgrade && \
    apt-get clean
RUN apt-get install --no-install-recommends -y ca-certificates curl git && \
    apt-get clean
