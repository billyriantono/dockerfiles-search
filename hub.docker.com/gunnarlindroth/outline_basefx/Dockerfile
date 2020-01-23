FROM openjdk:8

ENV TERM=xterm

RUN apt-get update && apt-get install --no-install-recommends -y \   
    less \
    tree \
    vim \
    net-tools \
    tcpdump \
    lksctp-tools \
    openjfx \
    && rm -rf /var/lib/apt/lists/*

