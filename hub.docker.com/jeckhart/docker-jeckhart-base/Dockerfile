FROM gentoo/stage3-amd64:latest
MAINTAINER John Eckhart "jeckhart@yodle.com"

ADD build/ /build/docker-jeckhart-base/

RUN /build/docker-jeckhart-base/prepare.sh && /build/docker-jeckhart-base/python.sh && /build/docker-jeckhart-base/cleanup.sh
