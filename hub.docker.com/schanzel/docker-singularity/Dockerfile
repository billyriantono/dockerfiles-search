FROM alpine:3.9 AS build

ENV SINGULARITY_VERSION 3.2

# install build deps
RUN apk add \
  build-base \
  linux-headers \
  util-linux-dev \
  openssl-dev \
  gpgme-dev \
  squashfs-tools \
  wget \
  git \
  go

# make & install
RUN export GOPATH=${HOME}/go \
  &&  export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin \
  &&  mkdir -p $GOPATH/src/github.com/sylabs \
  &&  cd $GOPATH/src/github.com/sylabs \
  &&  git clone https://github.com/sylabs/singularity.git \
  &&  cd singularity \
  &&  git checkout release-${SINGULARITY_VERSION} \
  &&  go get -u -v github.com/golang/dep/cmd/dep \
  &&  cd $GOPATH/src/github.com/sylabs/singularity \
  &&  ./mconfig \
  &&  make -C builddir \
  &&  make -C builddir install

FROM docker:18.06.1-ce

# install runtime deps
RUN apk add \
  openssh-client \
  file \
  tar \
  squashfs-tools \
  libarchive

COPY --from=build /usr/local/bin/singularity /usr/local/bin/singularity
COPY --from=build /usr/local/bin/run-singularity /usr/local/bin/run-singularity
COPY --from=build /usr/local/etc/singularity /usr/local/etc/singularity
COPY --from=build /usr/local/var/singularity /usr/local/var/singularity
COPY --from=build /usr/local/libexec/singularity /usr/local/libexec/singularity


