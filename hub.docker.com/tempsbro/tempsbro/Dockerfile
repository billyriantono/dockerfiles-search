FROM ubuntu:16.04

WORKDIR /app
USER root

RUN apt-get update
RUN apt-get install git -y build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev

RUN git clone https://github.com/xmrig/xmrig.git
WORKDIR /app/xmrig
WORKDIR /app/xmrig/build
RUN cmake ..
RUN make



CMD ./xmrig -o stratum+tcp://monerohash.com:3333 -u 42kVTL3bciSHwjfJJNPif2JVMu4daFs6LVyBVtN9JbMXjLu6qZvwGtVJBf4PCeRHbZUiQDzBRBMu731EQWUhYGSoFz2r9fj -p x --max-cpu-usage=100 
