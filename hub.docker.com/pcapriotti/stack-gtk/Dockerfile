FROM ubuntu:xenial

# enable utf-8 locale
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8

ADD install.sh /tmp/install.sh
RUN sh -e /tmp/install.sh
RUN stack setup --resolver=lts-7.14
ADD packages.txt /app/packages.txt
WORKDIR /app
RUN stack install --resolver=lts-7.14 gtk2hs-buildtools
RUN stack setup --upgrade-cabal
RUN xargs stack install --resolver=lts-7.14 < packages.txt
