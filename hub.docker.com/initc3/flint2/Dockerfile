FROM buildpack-deps:buster

RUN apt-get update && apt-get install -y --no-install-recommends \
        libmpfr-dev \
	&& rm -rf /var/lib/apt/lists/*

RUN set -ex \
        \
        && mkdir -p /usr/src/flint2 \
        && git clone https://github.com/wbhart/flint2.git /usr/src/flint2 \
	    \
        && cd /usr/src/flint2 \
        && ./configure \
        && make \
        && make check \
        && make install \
        && rm -rf /usr/src/flint2
