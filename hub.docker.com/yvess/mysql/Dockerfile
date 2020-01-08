FROM mysql:5
MAINTAINER Yves Serrano <y@yas.ch>
RUN apt-get update && apt-get install -yq \
        procps \
        less \
        vim && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY docker-entrypoint.sh /entrypoint.sh
