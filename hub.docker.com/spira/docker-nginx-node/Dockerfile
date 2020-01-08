FROM spira/docker-nginx:2.0.1

MAINTAINER "Andre Lackmann" <andre@lackmann.net>

RUN apt-get update && \
    apt-get install -y \
    curl

RUN curl -sL https://deb.nodesource.com/setup_5.x | bash

RUN apt-get install -y nodejs

ENTRYPOINT ["/opt/bin/nginx-start.sh"]