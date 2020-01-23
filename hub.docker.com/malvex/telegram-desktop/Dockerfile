FROM ubuntu:xenial

RUN apt-get update && apt-get -y install wget tar xz-utils \
  libxcb1 libx11-6 libx11-xcb1 libdbus-1-3 libglib2.0-0

RUN wget https://telegram.org/dl/desktop/linux -O /tmp/tsetup.tar.xz \
  && tar xf /tmp/tsetup.tar.xz -C /tmp \
  && mv /tmp/Telegram/Telegram /usr/local/bin/Telegram \
  && rm -r /tmp/Telegram /tmp/tsetup.tar.xz

RUN useradd -m app
USER app

ENTRYPOINT ["/usr/local/bin/Telegram"]
