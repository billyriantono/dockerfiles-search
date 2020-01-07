from ubuntu

RUN \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    python \
    build-essential \
    ca-certificates \
    curl

ENV LIBRDKAFKA_VERSION 0.11.6
RUN curl -Lk -o /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz https://github.com/edenhill/librdkafka/archive/v${LIBRDKAFKA_VERSION}.tar.gz && \
    tar -xzf /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz -C /root && \
    cd /root/librdkafka-${LIBRDKAFKA_VERSION} && \
    ./configure --prefix=/usr && make && make install && make clean && rm -rf /root/librdkafka-${LIBRDKAFKA_VERSION}*
