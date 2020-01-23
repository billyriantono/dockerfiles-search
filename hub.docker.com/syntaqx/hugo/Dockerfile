FROM ubuntu:18.04

RUN DEBIAN_FRONTEND=noninteractive apt-get -qq update && \
  apt-get install -y --no-install-recommends \
    git \
    ca-certificates \
    asciidoc \
    curl \
    python3-pip \
  && pip3 install pygments \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/*

ENV HUGO_VERSION 0.56.3
ENV HUGO_BINARY hugo_${HUGO_VERSION}_Linux-64bit.deb

RUN curl -sL -o /tmp/hugo.deb \
    https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY} \
  && dpkg -i /tmp/hugo.deb \
  && rm /tmp/hugo.deb \
  && mkdir /usr/share/blog

WORKDIR /app
VOLUME ["/app"]

CMD ["hugo"]
