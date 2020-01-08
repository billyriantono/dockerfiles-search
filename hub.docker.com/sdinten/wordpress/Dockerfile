FROM wordpress
LABEL maintainer="Sander van Dinten <sander@vandinten.nl>"

RUN apt-get update && \
    apt-get install -y libgd3 libgd-dev && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd
