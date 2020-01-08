FROM ubuntu:16.04

WORKDIR /app

RUN apt-get update
RUN apt-get install -y git build-essential cmake libuv1-dev libssl-dev libhwloc-dev
RUN git clone https://github.com/bigbangcore/miner.git /app
RUN mkdir /app/build
RUN cmake .
RUN make


ENTRYPOINT ["./xmrig"]

