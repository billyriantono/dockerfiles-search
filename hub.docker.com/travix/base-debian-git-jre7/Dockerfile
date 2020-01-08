FROM travix/base-debian-git:latest

MAINTAINER Travix

# install dependencies
RUN apt-get update \
    && apt-get install -y \
        openjdk-7-jre-headless \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*