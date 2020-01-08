# Go cross compiler (xgo): Go 1.8.3
# Copyright (c) 2017 Péter Szilágyi. All rights reserved.
#
# Released under the MIT license.

FROM ykyuen/xgo-base

MAINTAINER Péter Szilágyi <peterke@gmail.com>

# Configure the root Go distribution and bootstrap based on it
ENV GO_VERSION 184

RUN \
  export ROOT_DIST=https://storage.googleapis.com/golang/go1.8.4.linux-amd64.tar.gz     && \
  export ROOT_DIST_SHA=0ef737a0aff9742af0f63ac13c97ce36f0bbc8b67385169e41e395f34170944f && \
  \
  $BOOTSTRAP_PURE
