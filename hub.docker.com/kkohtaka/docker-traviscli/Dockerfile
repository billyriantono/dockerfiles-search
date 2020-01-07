# Copyright 2016, Kazumasa Kohtaka. All rights reserved.

FROM ubuntu:16.04
MAINTAINER Kazumasa Kohtaka "kkohtaka@gmail.com"

RUN apt-get update && apt-get install -y \
        build-essential \
        ruby \
        ruby-dev \
    && rm -rf /var/lib/apt/lists/* \
    && ruby -v \
    && gem install travis -v 1.8.2 --no-rdoc --no-ri \
    && travis version

ENTRYPOINT ["travis"]
CMD ["--help"]
