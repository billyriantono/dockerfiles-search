FROM stadlerb/halvm-fedora-runtime
MAINTAINER Bernhard Stadler <stadlerb@users.noreply.github.com>

# Compile install the HaNS from github.
USER root

# Install HaNS
WORKDIR /build
RUN git clone https://github.com/GaloisInc/HaNS.git\
    && cd /build/HaNS\
    && halvm-cabal -j1 install


WORKDIR /build
CMD /usr/bin/bash
