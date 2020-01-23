FROM quay.io/pypa/manylinux2010_x86_64

RUN curl -fSL https://github.com/Kitware/CMake/releases/download/v3.16.0-rc4/cmake-3.16.0-rc4-Linux-x86_64.sh -o cmake-3.16.0-rc4-Linux-x86_64.sh \
    && bash cmake-3.16.0-rc4-Linux-x86_64.sh --skip-license --prefix=/usr/local/ \
    && rm -f cmake-3.16.0-rc4-Linux-x86_64.sh
