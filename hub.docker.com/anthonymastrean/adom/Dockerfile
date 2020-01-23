FROM debian:stretch-slim

LABEL maintainer "Anthony Mastrean <anthony.mastrean@gmail.com>"

ENV TERM xterm-256color

RUN useradd -m adom
WORKDIR /home/adom
VOLUME /home/adom/.adom.data
USER adom

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        libncurses5 \
        tar \
    && curl -sS http://www.ancardia.com/download/adom_linux_debian_64_3.0.6.tar.gz \
        | tar -xz --strip-components 1 \
    && savedPackages="libncurses5" \
    && apt-mark auto '.*' > /dev/null \
    && apt-mark manual $savedPackages \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && rm -rf /var/cache/apt/* /var/lib/apt/lists/*

ENTRYPOINT ["./adom"]
