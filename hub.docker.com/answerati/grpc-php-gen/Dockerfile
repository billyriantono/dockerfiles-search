FROM php:7.0

ENV GRPC_RELEASE_TAG 1.6.0
ENV PROTOBUFF_RELEASE_TAG 3.4.0

RUN apt-get update \
    && apt-get install --yes git build-essential zip unzip automake libtool libz-dev wget \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install grpc-${GRPC_RELEASE_TAG}
RUN docker-php-ext-enable grpc

RUN pecl install protobuf-${PROTOBUFF_RELEASE_TAG}
RUN docker-php-ext-enable protobuf

WORKDIR /tmp

RUN wget https://github.com/google/protobuf/releases/download/v${PROTOBUFF_RELEASE_TAG}/protoc-${PROTOBUFF_RELEASE_TAG}-linux-x86_64.zip \
    && unzip protoc-${PROTOBUFF_RELEASE_TAG}-linux-x86_64.zip -d /opt/protoc \
    && rm protoc-${PROTOBUFF_RELEASE_TAG}-linux-x86_64.zip

ENV PATH $PATH:/opt/protoc/bin

RUN git clone -b v${GRPC_RELEASE_TAG} https://github.com/grpc/grpc \
    && cd grpc \
    && git submodule update --init \
    && make grpc_php_plugin \
    && mkdir -p /opt/grpc \
    && mv /tmp/grpc/bins/opt /opt/grpc/bin \
    && rm -rf /tmp/*

WORKDIR /root
