FROM meteogrid/base-linux-x86_64:latest

##############################################################################
# Install APKs we need to build stuff and configure image
##############################################################################

ENV PACKAGES="\
  linux-headers \
  g++ \
  paxctl \
  sudo \
  git \
  cmake \
  make \
  ca-certificates \
  llvm3.7 \
  py-pip \
  musl-dev \
  fftw-dev \
  libffi-dev \
  ncurses-dev \
  nodejs@edge \
  cabal@meteogrid \
  cairo-dev@meteogrid \
  curl-dev@meteogrid \
  libcurl@meteogrid \
  fontconfig-dev@meteogrid \
  freetype-dev@meteogrid \
  gdal-dev@meteogrid \
  geos-dev@meteogrid \
  ghc@meteogrid \
  ghcjs@meteogrid \
  giflib-dev@meteogrid \
  graphite2-dev@meteogrid \
  harfbuzz-dev@meteogrid \
  libecwj2-dev@meteogrid \
  libwebp-dev@meteogrid \
  libxml2-dev@meteogrid \
  llvm@meteogrid \
  llvm-dev@meteogrid \
  llvm-libs@meteogrid \
  llvm-static@meteogrid \
  pixman-dev@meteogrid \
  postgresql-dev@meteogrid \
  postgresql-client@meteogrid \
  postgresql-libs@meteogrid \
  libpq@meteogrid \
  proj4-dev@meteogrid \
  sqlite-dev@meteogrid \
  zlib-dev@meteogrid \
  boost@meteogrid \
  cairo@meteogrid \
  curl@meteogrid \
  fontconfig@meteogrid \
  freetype@meteogrid \
  gdal@meteogrid \
  py-gdal@meteogrid \
  geos@meteogrid \
  py-geos@meteogrid \
  ghc@meteogrid \
  giflib@meteogrid \
  graphite2@meteogrid \
  harfbuzz@meteogrid \
  icu@meteogrid \
  icu-dev@meteogrid \
  icu-libs@meteogrid \
  libecwj2@meteogrid \
  libwebp@meteogrid \
  libxml2@meteogrid \
  pixman@meteogrid \
  postgresql@meteogrid \
  libpq@meteogrid \
  proj4@meteogrid \
  sqlite@meteogrid \
  zlib@meteogrid \
  boost-dev@meteogrid \
  boost@meteogrid \
  mapnik-dev@meteogrid \
  mapnik@meteogrid \
  "

COPY unistd.patch stdlib.patch /tmp/

RUN apk --update --no-cache upgrade \
  && apk add --update --no-cache $PACKAGES \
  && pip --no-cache-dir install ipython \
  && cd /usr/include \
  && patch -i /tmp/unistd.patch \
  && patch -i /tmp/stdlib.patch \
  && rm /tmp/*.patch \
  && adduser -g "Meteogrid" -s /bin/ash -D meteogrid \
  && echo "meteogrid ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && cd /tmp \
  && git clone --depth=1 https://github.com/albertov/hs-mapnik \
  && cd hs-mapnik/mapnik_c \
  && cmake . -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_SHARED_LIBS=YES \
  && make \
  && sudo make install \
  && cmake . -DCMAKE_INSTALL_PREFIX=/usr -DBUILD_SHARED_LIBS=NO \
  && make \
  && sudo make install \
  && rm -rf /tmp/hs-mapnik

USER meteogrid
WORKDIR /home/meteogrid

ENV PATH=/home/meteogrid/.cabal/bin:$PATH

##############################################################################
# Install tools whe need to build haskell stuff
##############################################################################

COPY lts-7.4-cabal.config /tmp/cabal.config
RUN cd /tmp                                                                   \
 && cabal update                                                              \
 && cabal install happy alex                                                  \
 && cabal install gtk2hs-buildtools hscolour c2hs hspec-discover hoogle
