FROM alpine:3.8

RUN apk update && apk upgrade

RUN apk add python \
			      python-dev \
            py-pip \
            cmake \
            gcc \
            glib-dev \
            libsm \
            libxext \
            fontconfig \
            libxrender \
            libstdc++ \
            libc6-compat \
            glib \
            musl-dev \
            build-base \
            linux-headers

RUN pip install --upgrade pip \
    && pip install --no-cache-dir numpy

WORKDIR /
ENV OPENCV_VERSION="3.4.2"
RUN wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip \
&& unzip ${OPENCV_VERSION}.zip \
&& mkdir /opencv-${OPENCV_VERSION}/cmake_binary \
&& cd /opencv-${OPENCV_VERSION}/cmake_binary \
&& cmake -DBUILD_TIFF=ON \
  -DBUILD_opencv_java=OFF \
  -DWITH_CUDA=OFF \
  -DWITH_OPENGL=ON \
  -DWITH_OPENCL=ON \
  -DWITH_IPP=ON \
  -DWITH_TBB=ON \
  -DWITH_EIGEN=ON \
  -DWITH_V4L=ON \
  -DBUILD_TESTS=OFF \
  -DBUILD_PERF_TESTS=OFF \
  -DCMAKE_BUILD_TYPE=RELEASE \
  -DCMAKE_INSTALL_PREFIX="/usr" \
  -DPYTHON_EXECUTABLE="/usr/bin/python" \
  -DPYTHON_INCLUDE_DIR="/usr/include/python2.7" \
  -DPYTHON_PACKAGES_PATH="/usr/lib/python2.7/site-packages" \
  .. \
  && make install \
  && rm /${OPENCV_VERSION}.zip \
  && rm -r /opencv-${OPENCV_VERSION}

RUN python -c "import cv2; cv2.__version__"