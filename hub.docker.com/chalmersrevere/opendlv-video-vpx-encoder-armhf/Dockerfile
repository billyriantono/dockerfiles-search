# Copyright (C) 2018  Christian Berger
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

# Part to build opendlv-video-vpx-encoder.
FROM pipill/armhf-alpine:edge as builder
MAINTAINER Christian Berger "christian.berger@gu.se"

RUN [ "cross-build-start" ]

RUN apk update && \
    apk --no-cache add \
        diffutils \
        cmake \
        g++ \
        git \
        libx11-dev \
        make \
        perl \
        wget \
        yasm
RUN cd tmp && \
    git clone --depth 1 https://chromium.googlesource.com/libyuv/libyuv && \
    cd libyuv &&\
    make -f linux.mk libyuv.a && cp libyuv.a /usr/lib && cd include && cp -r * /usr/include
RUN cd tmp && \
    git clone --depth 1 --branch v1.7.0 https://github.com/webmproject/libvpx.git && \
    mkdir build && cd build && \
    ../libvpx/configure --disable-docs --disable-tools --enable-vp8 --enable-vp9 --enable-libyuv --disable-unit-tests --disable-webm-io --disable-postproc && \
    make -j4 && make install
ADD . /opt/sources
WORKDIR /opt/sources
RUN mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/tmp .. && \
    make && make install

RUN [ "cross-build-end" ]


# Part to deploy opendlv-video-vpx-encoder.
FROM pipill/armhf-alpine:edge
MAINTAINER Christian Berger "christian.berger@gu.se"

WORKDIR /usr/bin
COPY --from=builder /tmp/bin/opendlv-video-vpx-encoder .
ENTRYPOINT ["/usr/bin/opendlv-video-vpx-encoder"]

