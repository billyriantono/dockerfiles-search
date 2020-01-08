FROM ubuntu:xenial-20170214 

ENV MONO_VERSION 4.8.0.495
ENV MONO_TLS_PROVIDER=btls

RUN PREFIX="/home/mono" \ 
	&& mkdir $PREFIX \
	&& chown -R `whoami` $PREFIX \
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y  --no-install-recommends \
				git \ 
                autoconf \
                libtool \
                automake \
                build-essential \
				gettext \ 
                cmake  \
				ca-certificates-mono \
				curl\ 
				wget\
				gpac\
				davfs2\
	&& PATH=$PREFIX/bin:$PATH \
	&& git clone https://github.com/mono/mono.git \
	&& cd mono \
	&& ./autogen.sh --prefix=$PREFIX \
	&& make get-monolite-latest \
#	&& echo "Starting make with $(($(nproc)+1)) jobs..." \
	&& make \
	&& make install \
# remove packages which were used to compile mono but are not needed anymore
	&& apt-get remove -y \
	   autoconf \
	   automake \
	   build-essential \
	   git \
	   libtool \
	   wget \
	&& apt-get autoremove -y \
	&& apt-get clean \
	&& rm -rf /mono \
	&& curl -L -o /tmp/cacert.pem https://curl.haxx.se/ca/cacert.pem \
	&& cert-sync /tmp/cacert.pem \
	&& rm -rf /var/lib/apt/lists/*
