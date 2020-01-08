FROM glek/debian-node:latest

# Install package signing key
RUN wget --quiet -O - https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -

# Install package sources
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install latest Yarn
RUN apt-get update && \
    apt-get -y install --no-install-recommends yarn && \
    # Clean up cache
    rm -rf /var/lib/apt/lists/*
