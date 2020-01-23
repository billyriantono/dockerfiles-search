# Based on https://github.com/frol/docker-alpine-python-machinelearning
FROM guitarmind/python-nginx
MAINTAINER markpeng@exosite.com

RUN apk update && \
    apk add --no-cache \
        --virtual=.build-dependencies \
        g++ gfortran file binutils \
        musl-dev python3-dev cython openblas-dev \
        build-base freetype-dev libpng-dev \
        libffi-dev openssl-dev \
        llvm-dev \
        && \

    apk add libstdc++ openblas \
        && \

    ln -s locale.h /usr/include/xlocale.h \
        && \

    # Minimum required packages
    pip install Cython \
        numpy \
        pandas \
        scipy \
        && \

    # Dependency packages
    pip install scikit-learn \
        matplotlib \
        statsmodels \
        PyWavelets \
        librosa \
        psutil \
        && \

    # Model hosting related packages
    pip install flask \
        gevent \
        gunicorn \
        requests \
        && \

    # Cleanup
    rm -rf /var/cache/apk/* && \

    rm -r /root/.cache && \
    find /usr/lib/python3.*/ -name 'tests' -exec rm -r '{}' + && \
    find /usr/lib/python3.*/site-packages/ -name '*.so' -print -exec sh -c 'file "{}" | grep -q "not stripped" && strip -s "{}"' \; \
        && \

    rm /usr/include/xlocale.h \
        && \
    apk del .build-dependencies
