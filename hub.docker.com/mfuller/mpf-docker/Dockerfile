FROM alpine:3.5

RUN apk update \
&& apk add \
    ca-certificates \
    libstdc++ \
    libgfortran \
    python3 \
    build-base \
    py3-pillow \
    sdl2-dev \
    sdl2_ttf-dev \
    sdl2_image-dev \
    sdl2_mixer-dev \
    gstreamer1-dev \
    git \
&& apk add --virtual=build_dependencies \
    gfortran \
    g++ \
    gcc \
    make \
    python3-dev \
&& ln -s /usr/include/locale.h /usr/include/xlocale.h \
&& mkdir -p /tmp/build \
&& cd /tmp/build/ \
&& wget http://www.netlib.org/blas/blas-3.6.0.tgz \
&& wget http://www.netlib.org/lapack/lapack-3.6.1.tgz \
&& tar xzf blas-3.6.0.tgz \
&& tar xzf lapack-3.6.1.tgz \
&& cd /tmp/build/BLAS-3.6.0/ \
&& gfortran -O3 -std=legacy -m64 -fno-second-underscore -fPIC -c *.f \
&& ar r libfblas.a *.o \
&& ranlib libfblas.a \
&& mv libfblas.a /tmp/build/. \
&& cd /tmp/build/lapack-3.6.1/ \
&& sed -e "s/frecursive/fPIC/g" -e "s/ \.\.\// /g" -e "s/^CBLASLIB/\#CBLASLIB/g" make.inc.example > make.inc \
&& make lapacklib \
&& make clean \
&& mv liblapack.a /tmp/build/. \
&& cd / \
&& export BLAS=/tmp/build/libfblas.a \
&& export LAPACK=/tmp/build/liblapack.a \
&& python3 -m pip --no-cache-dir install pip -U \
&& python3 -m pip --no-cache-dir install scipy \
&& pip3 install --upgrade pip \
&& pip3 install -I Cython==0.24.1 \ 
&& pip3 install kivy matplotlib \ 
&& pip3 install --pre mpf mpf-mc \ 
&& apk del sdl2-dev sdl2_ttf-dev sdl2_image-dev sdl2_mixer-dev gstreamer1-dev \
&& rm -rf .cache \ 
&& apk del --purge -r build_dependencies \
&& rm -rf /tmp/build \
&& rm -rf /var/cache/apk/* \
&& mkdir /mpf

WORKDIR /mpf
CMD mpf


