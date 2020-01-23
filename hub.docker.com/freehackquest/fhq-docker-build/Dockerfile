FROM debian:10
WORKDIR /root/

LABEL "maintainer"="FreeHackQuest Team <freehackquest@gmail.com>"
LABEL "repository"="https://github.com/freehackquest/fhq-docker-build"

RUN apt-get update && \
    apt-get install -y curl

RUN curl -sL https://deb.nodesource.com/setup_12.x -o setup_node_12x.sh && bash setup_node_12x.sh

# basic libs
RUN apt-get update && apt-get install -y --no-install-recommends \
    make cmake \
    gcc g++ \
    curl \
    pkg-config \
    libcurl4-openssl-dev \
    zlibc zlib1g zlib1g-dev \
    libpng-dev \
    default-libmysqlclient-dev \ 
    libwebsockets-dev \
    apt-utils \
    gcc g++ \
    build-essential \
    nodejs

# RUN node --version
# RUN npm --version

RUN apt-get install -y --no-install-recommends \
    libqt5sql5-mysql \
    libqt5websockets5 \
    libqt5websockets5-dev \
    qt5-default \
    qtchooser

COPY ./npm-cache.sh ./npm-cache.sh
RUN ./npm-cache.sh
RUN apt-get clean