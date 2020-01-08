FROM debian:10-slim
ARG MINGW_ARCH=i686

# install cross compiler
RUN apt-get update && \
    apt-get install -y apt-utils && \
    apt-get install -y autoconf automake binutils \
                       cross-gcc-dev \
                       mingw-w64-${MINGW_ARCH}-dev \
                       g++-mingw-w64-${MINGW_ARCH} \
                       gfortran-mingw-w64-${MINGW_ARCH} \
                       binutils-mingw-w64-${MINGW_ARCH} && \
    apt-get clean

WORKDIR /workdir
VOLUME ["/workdir"]
CMD ["bash"]

