FROM debian:10

ARG VERSION=13.x

# Install required tools
RUN apt-get update && \
    apt-get -y install --no-install-recommends ca-certificates wget gnupg2 apt-utils && \
    # Clean up cache
    rm -rf /var/lib/apt/lists/*

# Install NodeSource package signing key
RUN wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -

# Install package sources
RUN echo "deb https://deb.nodesource.com/node_${VERSION} buster main" | tee /etc/apt/sources.list.d/nodesource.list && \
    echo "deb-src https://deb.nodesource.com/node_${VERSION} buster main" | tee -a /etc/apt/sources.list.d/nodesource.list

# Install latest NodeJS and NPM
RUN apt-get update && \
    apt-get -y install --no-install-recommends nodejs && \
    # Clean up cache
    rm -rf /var/lib/apt/lists/*
