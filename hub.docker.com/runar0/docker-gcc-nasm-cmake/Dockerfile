FROM gcc:8

RUN curl https://cmake.org/files/v3.13/cmake-3.13.0-Linux-x86_64.sh -o /tmp/curl-install.sh \
      && chmod u+x /tmp/curl-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/curl-install.sh --skip-license \
      && rm /tmp/curl-install.sh \
      && curl https://www.nasm.us/pub/nasm/releasebuilds/2.14/nasm-2.14.tar.bz2 -o /tmp/nasm-2.14.tar.bz2 \
      && cd /tmp \
      && tar xvf /tmp/nasm-2.14.tar.bz2 \
      && cd nasm-2.14 \
      && ./configure  \
      && make  \
      && make install \
      && rm -r /tmp/nasm-2.14 \
      && rm /tmp/nasm-2.14.tar.bz2