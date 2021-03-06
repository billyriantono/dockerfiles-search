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


###############################################################################
# Hace shallow clones de las dependencias que viven en repos de git y las     #
# construye
###############################################################################

COPY checkout_commit /usr/local/bin/
COPY cabal.server.project src/server/cabal.project
COPY cabal.client.project src/client/cabal.project
COPY sigym4-sdk src/common/sigym4-sdk
RUN sudo chown -R meteogrid $HOME                                             \
 && : "Paquetes compartibles entre cliente y servidor"                        \
 && cd $HOME/src/common                                                       \
 && checkout_commit a3eea07b60c53352d79075ef36d942f1817613be                  \
                    https://github.com/AccelerateHS/accelerate                \
 && checkout_commit 5f80b9ee3f79ca527026d87bdd253f1b23215828                  \
                    https://github.com/albertov/sigym4-geometry               \
 && checkout_commit 47d6ca7bb13281db4ce794233e49bca02b2c9d6f                  \
                    https://github.com/albertov/spatial-reference             \
 && checkout_commit 63ef22f1d01a9515e5c21693af4d38fa2ec6b2c1                  \
                    https://github.com/albertov/behave-hs                     \
 && checkout_commit f1e627b1a19f76fdf962348f2fce92099bf3d806                  \
                    https://github.com/bjornbm/dimensional                    \
 && : "Paquetes solo para cliente (por ser bindings a JS)"                    \
 && cd $HOME/src/client                                                       \
 && checkout_commit 50d298cb1b5ed850ec017e2aab10ffa1fb5466b0                  \
                    https://github.com/reflex-frp/reflex                      \
 && checkout_commit 8d203761ab4cbdb2060a48d980fbb6acbce21c5d                  \
                    https://github.com/reflex-frp/reflex-dom                  \
 && checkout_commit b52338c2dcd3b0707bc8aff2e171411614d4aed                   \
                    https://github.com/ghcjs/ghcjs-ffiqq                      \
 && checkout_commit 51413fbec37b0c3f3096996c8e8e6c0b780a1e24                  \
                    https://github.com/meteogrid/servant-reflex               \
 && : "A construir cliente"                                                   \
 && cabal --ghcjs new-build sigym4-sdk                                        \
 && : "Paquetes solo para ejecutar en servidor (por ser bindings a C/etc..)"  \
 && cd $HOME/src/server                                                       \
 && checkout_commit 529f9bf117b5ffd1ccf7ebeb679a97b3b1c67938                  \
                    https://github.com/bscarlet/llvm-general                  \
 && checkout_commit ef5901fde62f022ba05539ee47f859a7629ad449                  \
                    https://github.com/AccelerateHS/accelerate-llvm           \
 && checkout_commit f1bd266f14089106fa83733ec8b1234306f96299                  \
                    https://github.com/albertov/hs-mapnik                     \
 && checkout_commit f32285b20eaafebc9af657317b438a8c10dc2978                  \
                    https://github.com/albertov/bindings-gdal                 \
 && : "A construir servidor"                                                  \
 && : "Construye versiones enlazadas estaticamente de los bindings para "     \
 && : "verificar que todas las dependencias estan bien construidas e "        \
 && : "instaladas"                                                            \
 && cabal new-build --disable-optimization -fstatic bindings-gdal             \
 && cabal new-build --disable-optimization -fstatic hs-mapnik                 \
 && cabal new-build sigym4-sdk                                                


#&&                                                                           \
