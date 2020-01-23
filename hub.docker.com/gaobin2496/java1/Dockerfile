FROM	ubuntu:15.04
RUN	apt-get -y update && apt-get install -y \
	wget \
	git \
	build-essential \
	libssl-dev \
	libdb++-dev \
	libboost-all-dev \
	libqrencode-dev \
	libminiupnpc-dev \
	libtool \
	autotools-dev \
	autoconf \
	pkg-config
RUN 	git clone https://github.com/bitcoin/secp256k1.git /root/secp256k1
#RUN	chmod -R 777 /root/secp256k1
RUN	cd /root/secp256k1 && ./autogen.sh
RUN	cd /root/secp256k1 && ./configure
RUN	cd /root/secp256k1 && make
RUN	cd /root/secp256k1 && make install
CMD	bash
