FROM buildpack-deps:buster

ENV NTL_VERSION 11.4.1

RUN set -ex \
        \
        && wget -O ntl.tar.gz "https://www.shoup.net/ntl/ntl-$NTL_VERSION.tar.gz" \
        && mkdir -p /usr/src/ntl \
        && tar -xzC /usr/src/ntl --strip-components=1 -f ntl.tar.gz \
        && rm ntl.tar.gz \
	    \
	    && cd /usr/src/ntl/src \
        && ./configure CXXFLAGS="-g -O2 -fPIC -march=native -pthread -std=c++11" \
        && make \
        && make install \
        && rm -rf /usr/src/ntl
