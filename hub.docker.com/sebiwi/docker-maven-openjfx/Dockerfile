FROM maven:3.5.4-jdk-10

LABEL maintainer "Sebastian Caceres <contact.sebiwi@gmail.com>"

RUN apt-get update \
    && apt-get install --no-install-recommends -y \
        openjfx \
        unzip \
    && rm -f /var/lib/apt/lists/*_dists_*
