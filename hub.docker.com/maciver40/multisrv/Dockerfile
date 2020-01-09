FROM maciver40/ubuntu-base

LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/config" ]

RUN \
    apt-get update && \
    apt-get install -o DPkg::Options::="--force-confold" -y \
  	bind9 \
	bind9utils \
	chrony \
	easy-rsa \
	isc-dhcp-server \
	libssl-dev \
        openssl && \
     cd /opt && \
     git clone https://github.com/kvic-z/pixelserv-tls.git && \
     cd pixelserv-tls && \
     autoreconf -i && \
     ./configure && \
     make && \
     make install
