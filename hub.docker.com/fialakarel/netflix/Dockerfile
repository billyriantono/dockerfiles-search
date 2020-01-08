FROM ubuntu:18.10

MAINTAINER Karel Fiala <fiala.karel@gmail.com>

RUN apt-get update \
    && apt-get install --yes wget \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt install --yes ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && apt-get clean \
    && rm -rf /var/cache/* \
    && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/bin/google-chrome", "--no-sandbox", "https://www.netflix.com/cz/login"]
