FROM debian:jessie

RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    python \
    wget 

WORKDIR /root

RUN wget https://nodejs.org/dist/v4.2.4/node-v4.2.4-linux-x64.tar.gz
RUN tar xvzf node-v4.2.4-linux-x64.tar.gz
RUN mv node-v4.2.4-linux-x64 /node

WORKDIR /work

ENTRYPOINT ["/node/bin/node"]

