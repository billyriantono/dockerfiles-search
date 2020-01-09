FROM ubuntu:xenial

LABEL maintainer "Roman Dutchak <mr@c0x.io>"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        wget \
        curl \
        unzip

RUN \
  cd /opt && \
  wget https://musdcoin.com/assets/download/Linux_wallets.zip -O musdcoin.zip && \
  unzip musdcoin.zip && \
  mv Linux\ wallets/ musdcoin && \
  rm musdcoin.zip

RUN cp /opt/musdcoin/64/musdcoind /usr/local/bin/
RUN chmod +x /usr/local/bin/musdcoind

VOLUME ["/musdcoin"]
#
EXPOSE 9776 9777
#
COPY ["bin", "/usr/local/bin/"]
COPY ["docker-entrypoint.sh", "/usr/local/bin/"]
ENTRYPOINT ["docker-entrypoint.sh"]
