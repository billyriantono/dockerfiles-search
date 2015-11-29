FROM debian:8

MAINTAINER hudelmaier@gmail.com

RUN apt-get update
RUN apt-get install -y build-essential libpcre3 libpcre3-dev python wget

RUN wget -O /tmp/cppcheck-1.71.tar.gz https://github.com/danmar/cppcheck/archive/1.71.tar.gz
RUN cd /tmp/ && tar xvzf cppcheck-1.71.tar.gz

RUN cd /tmp/cppcheck-1.71 && make install SRCDIR=build CFGDIR=/cfg HAVE_RULES=yes

ENTRYPOINT ["cppcheck", "/src"]
