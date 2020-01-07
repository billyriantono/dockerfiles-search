# use alpine base
FROM python:3.7-alpine

# install and build zmq
# keep zmq-dev for .so
RUN apk update && \
    apk add --no-cache --virtual build-dependencies \
      g++ \
      python3-dev \
      linux-headers \
    && \
    apk add --no-cache \
      zeromq-dev \
    && \
    python3 -m pip install --no-cache-dir \
      pyzmq \
    && \
    apk del build-dependencies

RUN pip3 install --no-cache-dir \
       pyzmq
