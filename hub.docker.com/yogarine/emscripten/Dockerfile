FROM ubuntu:18.04

SHELL ["/bin/bash", "-c"]

# Install base dependencies
RUN apt-get update --yes --quiet && \
    apt-get install --yes curl build-essential git cmake python nodejs default-jre && \
    apt-get clean --yes --quiet && \
    rm --recursive --force /var/lib/apt/lists/*

# Instal Emscripten SDK
RUN cd /opt && \
    curl --silent https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz | tar --extract --gunzip --file -

# Update Emscripten
RUN cd /opt/emsdk-portable && \
    ./emsdk update && \
    ./emsdk install latest && \
    ./emsdk activate latest

# Run a test to see if everything is working properly and cache the required libraries.
RUN source /opt/emsdk-portable/emsdk_env.sh && cd $EMSCRIPTEN && python tests/runner.py test_exceptions_libcxx

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
