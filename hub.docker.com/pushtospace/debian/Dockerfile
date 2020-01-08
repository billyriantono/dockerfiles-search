FROM debian:jessie
MAINTAINER G.Jongenelen <g.jongenelen@pushto.space>

RUN echo "deb http://httpredir.debian.org/debian/ jessie-backports main contrib non-free" >> /etc/apt/sources.list && \
echo "deb-src http://httpredir.debian.org/debian/ jessie-backports main contrib non-free" >> /etc/apt/sources.list && \
apt-get update && apt-get upgrade -y && apt-get install -t jessie-backports wget zlib1g-dev build-essential libssl-dev=1.0.2k-1~bpo8+1 openssl=1.0.2k-1~bpo8+1 -y