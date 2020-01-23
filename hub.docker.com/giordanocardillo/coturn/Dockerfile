FROM phusion/baseimage
MAINTAINER Giordano Cardillo
RUN set -e; \
    apt-get update; \
    apt-get install -y coturn; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get clean;
CMD ["turnserver"]
