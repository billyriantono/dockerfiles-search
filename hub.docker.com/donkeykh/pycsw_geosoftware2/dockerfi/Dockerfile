FROM ubuntu:16.04

MAINTAINER Alexey Zhokhov <alexey@zhokhov.com>

ENV DEBIAN_FRONTEND noninteractive

# Update apt-get
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends \
               wget \
               ca-certificates \
               curl \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/* /var/cache/apt/* /tmp/*

RUN wget --no-cookies --no-check-certificate "https://bintray.com/artifact/download/omni/OmniBinaries/omnicore-0.3.0-x86_64-linux-gnu.tar.gz" \
    && tar -xzvf omnicore-0.3.0-x86_64-linux-gnu.tar.gz \
    && mkdir -p /opt \
    && mv omnicore-0.3.0 /opt/omnicore \
    && rm omnicore-0.3.0-x86_64-linux-gnu.tar.gz

VOLUME /data

COPY docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/opt/omnicore/bin/omnicored", "-conf=/data/bitcoin.conf"]
