FROM webdevops/php-nginx:7.2

LABEL maintainer="Alexander Pankov <pankov.ap@gmail.com>"

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
        libz-dev \
        openssl \
        unzip \
        rsync \
        lsyncd \
        coreutils \
        && \
    pecl install grpc && pecl install protobuf && \
    echo extension=protobuf.so >> /opt/docker/etc/php/php.ini && \
    echo extension=grpc.so >> /opt/docker/etc/php/php.ini && \
    rm -rf /var/lib/apt/lists/*