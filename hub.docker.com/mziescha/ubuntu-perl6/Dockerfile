FROM ubuntu:17.10

MAINTAINER Mario Zieschang <mziescha@cpan.org>

ENV ZEF_VERSION 'master'

RUN     apt-get update -y && apt-get upgrade -y \
    &&  apt-get install -y curl wget git perl6 \
    &&  curl -L https://github.com/ugexe/zef/archive/${ZEF_VERSION}.tar.gz | tar zxv \
    #&&  curl -L https://github.com/ugexe/zef/archive/v${ZEF_VERSION}.tar.gz | tar zxv \
    &&  cd /zef-${ZEF_VERSION} \
    &&  perl6 -Ilib bin/zef install . --force-test \
    &&  cd .. \
    &&  apt-get autoremove -y \
    &&  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /zef

ENV PATH /usr/share/perl6/site/bin:$PATH
