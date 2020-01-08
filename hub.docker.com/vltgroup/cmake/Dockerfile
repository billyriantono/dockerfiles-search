FROM ubuntu:16.04

RUN apt-get -qq update \
    && apt-get install -y --no-install-recommends --no-install-suggests cmake wget \
       g++ make libx11-dev libxi-dev libxrandr-dev libpcsclite-dev libboost1.58-all-dev libssl-dev cmake \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root

CMD ["cmake"]
