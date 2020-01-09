FROM ubuntu:16.04

RUN echo "deb http://repo.aptly.info/ squeeze main" > /etc/apt/sources.list.d/aptly.list \
    && apt-key adv --keyserver pool.sks-keyservers.net --recv-keys ED75B5A4483DA07C \
    && apt-get -qq update \
    && apt-get install -y --no-install-recommends --no-install-suggests aptly wget ca-certificates \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p -m 0700 /root/.gnupg/

COPY gpg.conf /root/.gnupg/
COPY aptly-publish.sh /usr/local/bin/

WORKDIR /root

CMD ["aptly"]
