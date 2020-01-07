FROM tcnksm/centos-buildpack-deps:6

RUN mkdir /usr/src/perl
WORKDIR /usr/src/perl

RUN curl -SL https://cpan.metacpan.org/authors/id/S/SH/SHAY/perl-5.20.1.tar.bz2 -o perl-5.20.1.tar.bz2 \
    && tar --strip-components=1 -xjf perl-5.20.1.tar.bz2 -C /usr/src/perl \
    && rm perl-5.20.1.tar.bz2

RUN ./Configure -Duse64bitall  -des \
        && make -j$(nproc) \
        && TEST_JOBS=$(nproc) make test_harness \
        && make install \
        && make veryclean

WORKDIR /usr/src
RUN curl -LO https://raw.githubusercontent.com/miyagawa/cpanminus/master/cpanm \
        && chmod +x cpanm \
        && ./cpanm App::cpanminus \
        && rm ./cpanm

WORKDIR /root

CMD ["perl5.20.1","-de0"]
