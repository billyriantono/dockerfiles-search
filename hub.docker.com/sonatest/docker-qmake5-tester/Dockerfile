FROM debian:stretch-slim

ENV DEBIAN_FRONTEND noninteractive

# install tools for compiling projects
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y --no-install-recommends --no-install-suggests \
							autoconf \
							ca-certificates \
							curl \
							git \
							make \
							patch \
							python \
							qt5-qmake \
							qt5-default \
							qtbase5-dev-tools \
							unzip \
							wget

RUN echo 'deb http://httpredir.debian.org/debian/ jessie main contrib non-free' >> /etc/apt/sources.list

RUN apt-get update \
	&& apt-get install -y --no-install-recommends --no-install-suggests \
							g++=4:4.9.2-2

ENV QTDIR=/opt/qt57
ENV PKG_CONFIG_PATH=$QTDIR/lib/pkgconfig:$PKG_CONFIG_PATH
# add QT to path and set variable for .QT_OVERRIDE_PATH 
ENV QT5_PATH="/opt/qt57/bin"
ENV PATH=$QT5_PATH:$PATH 

# create user under which to run the tests
RUN useradd --uid 1000 -G sudo --create-home tester && mkdir /home/tester/bin && chown -R tester:tester /home/tester/bin
ADD bin /home/tester/bin
ENV PATH=/home/tester/bin:$PATH

# installing ccache
RUN touch dev_mode_disabled
ADD ccache.patch ./ccache.patch

ENV CCACHE_VER=3.3.3
RUN wget https://github.com/ccache/ccache/archive/v${CCACHE_VER}.tar.gz \
	&& tar -xf v${CCACHE_VER}.tar.gz --strip-components=1 \
	&& rm v${CCACHE_VER}.tar.gz \
	&& ./autogen.sh

# Patch ccache to not build documentation
RUN patch -p1 -i ccache.patch \
	&& ./configure \
	&& make \
	&& make install

RUN mkdir -p /usr/local/lib/ccache
RUN ln -sf ../../bin/ccache /usr/local/lib/ccache/gcc \
	&& ln -sf ../../bin/ccache /usr/local/lib/ccache/g++ \
	&& ln -sf ../../bin/ccache /usr/local/lib/ccache/cc \
	&& ln -sf ../../bin/ccache /usr/local/lib/ccache/c++

ENV PATH=/usr/lib/ccache:$PATH

WORKDIR /home/tester/opt

# installing Google Test & Mock
ADD googletest-1.8.0.zip /home/tester/opt/googletest-1.8.0.zip
# install dependencies
RUN unzip -q googletest-1.8.0.zip -x "*/docs/*" -x "*/msvc/*" -x "*/samples/*" \
	&& rm googletest-1.8.0.zip && mv googletest-release-1.8.0 gtest \
	&& apt-get purge -y --auto-remove unzip 

ENV GTEST_ROOT=/home/tester/opt/gtest/googletest
ENV GTEST_DIR=${GTEST_ROOT} GMOCK_DIR=/home/tester/opt/gtest/googlemock 
ENV GTEST_INCLUDE_DIR=${GTEST_ROOT}/include 
ENV GMOCK_INCLUDE_DIR=/home/tester/opt/gtest/googlemock/include 
ENV GTEST_MAIN_LIBRARY=/home/tester/opt/gtest/libgmock.a 
ENV GTEST_LIBRARY=/home/tester/opt/gtest/libgmock.a

# Compiling GMock and GTest
# Version 1.7.0 expect library in GMOCK_DIR
RUN g++ -isystem ${GTEST_DIR}/include -I${GTEST_DIR} -isystem ${GMOCK_DIR}/include -I${GMOCK_DIR} -pthread -c ${GTEST_DIR}/src/gtest-all.cc \
	&& g++ -isystem ${GTEST_DIR}/include -I${GTEST_DIR} -isystem ${GMOCK_DIR}/include -I${GMOCK_DIR} -pthread -c ${GMOCK_DIR}/src/gmock-all.cc \
	&& ar -rv /home/tester/opt/gtest/libgmock.a gtest-all.o gmock-all.o \
	&& cp /home/tester/opt/gtest/libgmock.a ${GMOCK_DIR}/ \
	&& rm -rf /home/tester/opt/*/*.o

# Patch GMock
ADD gmock_tokenize_public_slots.patch /home/tester/opt/gtest/googlemock/scripts/generator/cpp/tokenize.patch
WORKDIR /home/tester/opt/gtest/googlemock/scripts/generator/cpp
RUN patch -p1 < ./tokenize.patch

# cleanup
# remove caches, documents, logs and examples
# remove build temp files & unused packages
# remove apt-(get/cache) package list
RUN find /opt \( -name "doc" -o -name "examples" \) -type d -print0 | xargs -0 --no-run-if-empty rm -rf \
	&& find /usr/share \( -name fonts -o -name "[hH]elp" -o -name man -o -name "[lL]ocale" \) -type d -print0 | xargs -0 --no-run-if-empty rm -rf \
	&& find /var/log -name "*" -type f -print0 | xargs -0 --no-run-if-empty rm -f -- \
	&& find /var/cache -name "*" -type f -print0 | xargs -0 --no-run-if-empty rm -f -- \
	&& apt-get clean \
	&& apt-get purge -y patch \
	&& apt-get -y autoclean \
	&& apt-get -y autoremove  \
	&& rm -rf /var/lib/apt/lists/* && rm -rf /var/lib/dpkg/info/*

ENV GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

USER tester

# Configuring ccache in user account
RUN ccache --set-config=cache_dir=/cache --max-size=10G

WORKDIR /dublin

