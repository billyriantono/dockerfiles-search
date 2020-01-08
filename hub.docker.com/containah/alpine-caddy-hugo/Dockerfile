FROM rjarow/alpine-caddy-s6
LABEL maintainer "Rich J github.com/rjarow" architecture="AMD64/x86_64"

ENV HUGO_VERSION=0.32.4

WORKDIR /tmp
RUN curl -L\
    https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
    #https://github.com/gohugoio/hugo/releases/download/v0.32.4/hugo_0.32.4_Linux-64bit.tar.gz \
    | tar --no-same-owner -C /usr/bin -xz hugo
