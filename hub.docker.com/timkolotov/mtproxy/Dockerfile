FROM ubuntu:latest
LABEL maintainer="Tim Kolotov <timophey.kolotov@gmail.com>"

    # install all dependencies
RUN apt-get -y update && apt-get -y install git curl iproute2 build-essential libssl-dev zlib1g-dev && \
    # get MTProxy from repository and build
    git clone https://github.com/TelegramMessenger/MTProxy && cd MTProxy && make && \
    # get Proxy Secret
    mkdir /etc/MTProxy && curl -s https://core.telegram.org/getProxySecret -o /etc/MTProxy/proxy-secret && \
    # copy binary
    cp ./objs/bin/mtproto-proxy /usr/local/bin/mtproto-proxy && \
    # cleanup
    apt-get -y autoremove git build-essential libssl-dev zlib1g-dev && \
    apt-get autoclean && rm -rf /MTProxy /var/lib/apt/lists

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
