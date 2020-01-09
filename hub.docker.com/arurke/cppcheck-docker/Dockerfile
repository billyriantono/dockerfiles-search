FROM python:3

RUN \
    apt-get update && \
    apt-get install -y git make g++ libpcre3 libpcre3-dev && \
    mkdir -p /usr/src /src && cd /usr/src && \
    git clone https://github.com/danmar/cppcheck.git && \
    cd cppcheck && \
    git checkout 1.88 && \
    make install SRCDIR=build CFGDIR=/cfg HAVE_RULES=yes CXXFLAGS='-O2 -DNDEBUG -Wall -Wno-sign-compare -Wno-unused-function' && \
    strip /usr/bin/cppcheck && \
    rm -rf /usr/src
