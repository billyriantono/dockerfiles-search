FROM stadlerb/halvm-fedora-base
MAINTAINER Bernhard Stadler <stadlerb@users.noreply.github.com>

# Clone 'master' of HaLVM and build it.
USER root

WORKDIR /build
RUN git clone https://github.com/GaloisInc/HaLVM.git\
    && cd /build/HaLVM\
    && git submodule update --init --recursive\
    && autoconf\
    && ./configure --prefix=/opt/halvm --enable-gmp\
    && make\
    && make install\
    && cd /build\
    && rm -rf /build/HaLVM\
    && cabal update

WORKDIR /build
CMD /usr/bin/bash
