FROM php:7.0

ENV GRPC_RELEASE_TAG 1.6.0
ENV PROTOBUFF_RELEASE_TAG 3.4.0

RUN apt-get update \
    && apt-get install --yes libz-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install grpc-$GRPC_RELEASE_TAG
RUN docker-php-ext-enable grpc

RUN pecl install protobuf-$PROTOBUFF_RELEASE_TAG
RUN docker-php-ext-enable protobuf
