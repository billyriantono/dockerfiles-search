FROM haskell:8.0.1
MAINTAINER radek.molenda@gmail.com

RUN mkdir /haskell_install
WORKDIR /haskell_install

ADD https://haskell.org/platform/download/8.0.1/haskell-platform-8.0.1-unknown-posix--full-x86_64.tar.gz .

RUN tar xf haskell-platform-8.0.1-unknown-posix--full-x86_64.tar.gz && ./install-haskell-platform.sh
