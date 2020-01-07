FROM buildpack-deps:jessie

##############################
## python 3.6.4
RUN apt-get purge -y python.*

ENV LANG C.UTF-8

ENV PYTHON_VERSION 3.6.4

ENV PYTHON_PIP_VERSION 8.1.1

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    build-essential  \
    vim \
    git \
    gfortran \
    liblapack-dev \
    gzip \
    bzip2 \
    cmake \
    python-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN set -ex \
    && curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" -o python.tar.xz \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f python.tar.xz \
    && rm python.tar.xz \
    && cd /usr/src/python \
    && ./configure --enable-shared --enable-unicode=ucs4 \
    && make -j$(nproc) \
    && make install \
    && ldconfig \
    && pip3 install --no-cache-dir --upgrade --ignore-installed pip==$PYTHON_PIP_VERSION \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && rm -rf /usr/src/python ~/.cache

RUN cd /usr/local/bin \
    && ln -s easy_install-3.5 easy_install \
    && ln -s idle3 idle \
    && ln -s pydoc3 pydoc \
    && ln -s python3 python \
    && ln -s python3-config python-config

##############################
## ffmpeg
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
RUN wget http://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz \
    && tar xvf ffmpeg-release-64bit-static.tar.xz \
    && cp ./ffmpeg-*/ffmpeg /usr/local/bin \
    && rm -rf /usr/src/app

##############################
## dlib
WORKDIR /root
RUN wget http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2 \
    && wget http://dlib.net/files/shape_predictor_5_face_landmarks.dat.bz2 \
    && wget http://dlib.net/files/dlib_face_recognition_resnet_model_v1.dat.bz2 \
    && bzip2 -d shape_predictor_68_face_landmarks.dat.bz2 \
    && bzip2 -d shape_predictor_5_face_landmarks.dat.bz2 \
    && bzip2 -d dlib_face_recognition_resnet_model_v1.dat.bz2

## requirements
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY requirements.txt /usr/src/app/
RUN pip3 install --no-cache-dir -r requirements.txt \
    && rm -rf /usr/src/app

