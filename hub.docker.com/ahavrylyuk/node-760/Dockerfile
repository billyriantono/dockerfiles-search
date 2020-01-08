FROM debian:jessie-slim

RUN apt-get update && apt-get install -y curl python build-essential \
  && curl -sS https://nodejs.org/dist/v7.6.0/node-v7.6.0.tar.gz | tar -xz \
  && cd node-v7.6.0 && ./configure && make -j4 && make install && rm -rf /node-v7.6.0