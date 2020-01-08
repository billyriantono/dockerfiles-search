# Import Base
FROM ubuntu:16.04

# Info
MAINTAINER Ian Naish <alixakz@gmail.com>

# Update & upgrade system
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get update \
    && apt-get -y dist-upgrade -u \
    && apt-get install -y wget vim git php-cli \
    && rm -rf /var/lib/apt/lists/*

# Timezone
RUN echo "Europe/London" | tee /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata