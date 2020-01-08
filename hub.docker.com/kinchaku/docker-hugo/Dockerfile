FROM debian:stable-slim
MAINTAINER git@getpanda.me

RUN apt-get -qq update \
	&& DEBIAN_FRONTEND=noninteractive apt-get -qq install -y --no-install-recommends libstdc++6 rsync openssh-client git ca-certificates curl \
	&& rm -rf /var/lib/apt/lists/*

ENV HUGO_VERSION 0.55.6
ENV HUGO_BINARY hugo_extended_${HUGO_VERSION}_Linux-64bit.deb

# Download and install hugo
RUN curl -sL -o /tmp/hugo.deb \
    https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY} && \
    dpkg -i /tmp/hugo.deb && \
    rm /tmp/hugo.deb
