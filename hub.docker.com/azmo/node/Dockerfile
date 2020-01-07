FROM azmo/base:debian-slim

RUN apt-get update && apt-get -y install --no-install-recommends gnupg && \
        curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | \
        apt-key add - && \
        echo "deb https://deb.nodesource.com/node_8.x stretch main" > \
            /etc/apt/sources.list.d/nodesource.list && \
        apt-get update && \
        apt-get install --no-install-recommends -y nodejs && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
