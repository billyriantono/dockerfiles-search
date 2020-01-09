FROM homeassistant/home-assistant:0.55.2
MAINTAINER James Grant <james@queeg.org>

RUN apt-get update && \
    apt-get install -y git && \
    git clone --depth 1 --recursive -b dtls https://github.com/home-assistant/libcoap.git && \
    cd libcoap && \
    ./autogen.sh && \
    ./configure --disable-documentation --disable-shared --without-debug CFLAGS="-D COAP_DEBUG_FD=stderr" && \
    make && \
    make install && \
    cd .. && rm -rf libcoap && \
    rm -rf /var/lib/apt/lists/*

