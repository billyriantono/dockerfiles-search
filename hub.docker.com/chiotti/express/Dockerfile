FROM ubuntu

RUN apt-get update && apt-get install -y \
    curl \
    libboost-all-dev \
    zlib1g-dev \
    bamtools

WORKDIR /opt

RUN curl -O https://pachterlab.github.io/eXpress/downloads/express-1.5.1/express-1.5.1-linux_x86_64.tgz \
    && tar -xzf express-1.5.1-linux_x86_64.tgz \
    && mv express-1.5.1-linux_x86_64/express /opt \
    && rm -rf express-1.5.1-linux_x86_64 express-1.5.1-linux_x86_64.tgz
