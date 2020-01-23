FROM igeolise/ubuntu:16.04

RUN apt-get update && \
    apt-get install -y build-essential && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -y nodejs && \
    apt-get install -y git && \
    npm install -g npm@5.3.0 && \
    apt-get install -y python && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /opt/npm/
