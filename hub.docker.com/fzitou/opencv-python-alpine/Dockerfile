FROM alpine:3.8

ENV OPENCV_VER 3.4.3
ENV OPENCV https://github.com/opencv/opencv/archive/${OPENCV_VER}.tar.gz
ENV CC /usr/bin/clang
ENV CXX /usr/bin/clang++

RUN apk add -U --no-cache --virtual=build-dependencies \
        linux-headers \
        build-base \
        musl \
        musl-dev \
        g++ \
        gcc \
        libgcc \
        libxml2-dev \
        libxslt-dev \
        libffi-dev \
        lcms2-dev \
        jpeg-dev \
        openjpeg-dev \
        openssl-dev \
        zlib-dev \
        freetype-dev \
        python3-dev \
        make \
        cmake \
        clang \
        clang-dev \
        ninja \
        curl \
    && apk add --no-cache \
        python3 \
        zlib \
        jpeg \
        libjpeg \
        openjpeg \
        freetype \
        tesseract-ocr \
    && curl https://bootstrap.pypa.io/get-pip.py | python3 \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && ln -s /usr/include/locale.h /usr/include/xlocale.h \
    && pip install -U --no-cache-dir \
        pip \
    && pip install -U --no-cache-dir \
        Pillow \
        pytesseract \
        numpy \
    && curl -L $OPENCV | tar zx \
    && (cd opencv-$OPENCV_VER \
    && mkdir build \
    && cd build \
    && cmake \
        -G Ninja \
        -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D WITH_FFMPEG=NO \
        -D WITH_IPP=NO \
        -D PYTHON_EXECUTABLE=/usr/bin/python \
        -D WITH_OPENEXR=NO .. \
    && ninja \
    && ninja install) \
    && ln -s /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so \
          /usr/lib/python3.6/site-packages/cv2.so \
    && apk del build-dependencies \
    && rm -rf /var/cache/apk/* /opencv-$OPENCV_VER
