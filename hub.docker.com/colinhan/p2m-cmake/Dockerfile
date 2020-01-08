FROM gcc:9

RUN curl -s \
    "https://cmake.org/files/v3.15/cmake-3.15.2-Linux-x86_64.tar.gz" \
      | tar --strip-components=1 -xz -C /usr/local

CMD gcc --version && cmake --version
