FROM ubuntu:18.04

RUN apt-get update -qq && apt-get install -qq -y dirmngr
RUN echo deb http://ppa.launchpad.net/visvirial/monacoin/ubuntu bionic main > /etc/apt/sources.list.d/visvirial-monacoin-artful.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 46F1E621FFD374E3 && \
    apt-get update -qq && \
    apt-get install -qq -y --no-install-recommends --allow-unauthenticated \
	    autoconf \
	    automake \
	    monacoind \
	    build-essential \
	    ca-certificates \
	    curl \
	    libbase58-dev \
	    libgmp-dev \
	    libprotobuf-c-dev \
	    libsodium-dev \
	    libsqlite3-dev \
	    zlib1g-dev \
	    libtool \
	    make \
	    net-tools \
	    python \
	    python3 \
      python3-mako \
	    valgrind \
	    git

RUN git clone https://github.com/monaco-ex/lightning.git -b pr-add-monacoin /opt/lightningd && \
    cd /opt/lightningd && \
    ./configure && \
    make && \
    cp lightningd/lightningd lightningd/lightning_* cli/lightning-cli /usr/bin/ && \
    rm -rf /opt/lightningd

ADD entrypoint.sh /

ENTRYPOINT /entrypoint.sh
CMD ['--port=9735' '--network=monacoin' '--log-level=debug']

VOLUME /root
