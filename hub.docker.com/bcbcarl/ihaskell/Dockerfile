FROM bcbcarl/archlinux
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

ENV HOME /root
ENV PATH $HOME/.cabal/bin:$PATH

# Prepare for build
RUN \
  pacman --noconfirm -S \
    zeromq ghc cabal-install git automake \
    libtool pkg-config python sqlite && \
  yes | pacman -Scc && pacman-optimize && \
  cabal update && \
  cabal install happy cpphs && \
  git clone https://github.com/gibiansky/IHaskell

# Build IHaskell
RUN cd IHaskell && ./build.sh all && cd - && rm -rf IHaskell

# Install IPython for IHaskell
RUN echo exit | IHaskell console