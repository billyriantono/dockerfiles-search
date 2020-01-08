
FROM ubuntu:trusty
MAINTAINER Chris Carpentier <coredump@gmail.com>

#ADD file:3037fa9e903e9ae5338ac1dd3adf8d3ff2d165d3a9b550c64879651582c77dc4 in /
#CMD "/bin/bash"

RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates curl wget && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends bzr git mercurial openssh-client subversion && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends autoconf automake bzip2 file g++ gcc imagemagick libbz2-dev libc6-dev libcurl4-openssl-dev libevent-dev libffi-dev libgeoip-dev libglib2.0-dev libjpeg-dev liblzma-dev libmagickcore-dev libmagickwand-dev libmysqlclient-dev libncurses-dev libpng-dev libpq-dev libreadline-dev libsqlite3-dev libssl-dev libtool libwebp-dev libxml2-dev libxslt-dev libyaml-dev make patch xz-utils zlib1g-dev && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y curl procps && rm -fr /var/lib/apt/lists/*

RUN mkdir /usr/src/perl

#COPY file:c8200406a5ee5be485187bfbbeb7f1c382915eed9e7f44333a436ced13aba0a9 in /usr/src/perl/

WORKDIR /usr/src/perl

RUN curl -SL https://cpan.metacpan.org/authors/id/R/RJ/RJBS/perl-5.22.0.tar.bz2 -o perl-5.22.0.tar.bz2 && \
      echo '400338c91c56420d98142cbfcb84d418cae2c98c *perl-5.22.0.tar.bz2' | sha1sum -c - && \
      tar --strip-components=1 -xjf perl-5.22.0.tar.bz2 -C /usr/src/perl && \
      rm perl-5.22.0.tar.bz2 && \
      cat *.patch | patch -p1 && \
      ./Configure -Duse64bitall -des && \
      make -j$(nproc) && make test_harness && make install && \
      cd /usr/src && \
      curl -LO https://raw.githubusercontent.com/miyagawa/cpanminus/master/cpanm && \
      chmod +x cpanm && \
      ./cpanm App::cpanminus && \
      rm -fr ./cpanm /root/.cpanm /usr/src/perl

#WORKDIR /root

#CMD "perl5.22.0" "-de0"
