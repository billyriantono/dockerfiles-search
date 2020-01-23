FROM debian:stretch-slim

LABEL maintainer "Anthony Mastrean <anthony.mastrean@gmail.com>"

WORKDIR /usr/src

RUN apt-get update \
    # && savedPackages="" \
    && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libncurses5-dev \
        tar \
    && curl -o smenu-0.9.14.tar.gz -ksJLOS https://github.com/p-gen/smenu/archive/v0.9.14.tar.gz \
    && tar xzf smenu-0.9.14.tar.gz \
    && rm -rf smenu-0.9.14.tar.gz \
    && cd smenu-0.9.14 \
    && ./build.sh \
    && make install \
    && cd .. \
    # && apt-mark auto '.*' > /dev/null \
    # && apt-mark manual $savedPackages \
    # && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -fr /var/cache/apt/* /var/lib/apt/lists/*

ENTRYPOINT ["smenu"]
