################################################################################
##  Dockerfile to build complete local development environemnt for OpenCV4   ###
##  with Python CPP JAVA                                                     ###
################################################################################
FROM alpine:3.10 as compiler

MAINTAINER Glitch

ENV LANG=C.UTF-8

# Add PKG Repositories
RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.10/main' >> /etc/apk/repositories && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/v3.10/community' >> /etc/apk/repositories

# Install Glibc
RUN apk --no-cache add ca-certificates wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk && \
    apk add glibc-2.29-r0.apk

# Install Necessary Dependencies
RUN apk add --update \
      --no-cache \
      build-base unzip curl wget git \
      clang clang-dev cmake pkgconf wget openblas openblas-dev \
      cmake pkgconfig \
      g++ libtbb libtbb-dev libwebp \
      libjpeg libavc1394 libavc1394-dev \
      libjpeg-turbo libjpeg-turbo-dev gstreamer gstreamer-dev \
      libpng libpng-dev openjdk11 \
      jasper-dev gst-plugins-base gst-plugins-base-dev \
      tiff tiff-dev libgphoto2 libgphoto2-dev \
      libwebp libwebp-dev python3 python3-dev python2 python2-dev libgfortran \
      gfortran py2-pip py3-pip build-base py3-numpy py2-numpy apache-ant \
      clang-dev openexr openexr-dev gtk+ gtk+-dev mesa mesa-dev \
      ffmpeg-libs ffmpeg-dev linux-headers tesseract-ocr && \
      rm -rf /var/cache/apk/*

# Making Links for binaries
RUN ln -vfs /usr/bin/python3 /usr/local/bin/python && \
    ln -vfs /usr/bin/pip3 /usr/local/bin/pip && \
    ln -vfs /usr/include/libpng16 /usr/include/libpng && \
    ln -vfs /usr/include/locale.h /usr/include/xlocale.h

# Install Scientific Dependencies
RUN pip3 --no-cache-dir install numpy pillow pytesseract && \
    pip2 --no-cache-dir install numpy pillow pytesseract && \
    pip3 --no-cache-dir install --upgrade numpy pillow pytesseract pandas && \
    pip2 --no-cache-dir install --upgrade numpy pillow pytesseract

# Set Environment Variables
ENV CC /usr/bin/clang
ENV CXX /usr/bin/g++
ENV OPENCV_VERSION='4.1.1' DEBIAN_FRONTEND=noninteractive
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk 

# OpenCV 4 Download and Extract
RUN mkdir -p /opt && cd /opt && \
  wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip && \
  unzip ${OPENCV_VERSION}.zip && \
  rm -rf ${OPENCV_VERSION}.zip

# OpenCV 4 Contrib Download and Extract
RUN  mkdir -p /opt && cd /opt && \
  wget https://github.com/opencv/opencv_contrib/archive/$OPENCV_VERSION.tar.gz && \
  tar -xvzf $OPENCV_VERSION.tar.gz && \
  rm -vrf $OPENCV_VERSION.tar.gz

# OpenCV 4 Build
RUN mkdir -p /opt/opencv-${OPENCV_VERSION}/build && \
  cd /opt/opencv-${OPENCV_VERSION}/build && \
  cmake \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D CMAKE_C_COMPILER=/usr/bin/clang \
    -D CMAKE_CXX_COMPILER=/usr/bin/clang++ \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-$OPENCV_VERSION/modules \
    -D BUILD_DOCS=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D BUILD_opencv_apps=OFF \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_SHARED_LIBS=OFF \ 
    -D BUILD_TESTS=OFF \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D ENABLE_PRECOMPILED_HEADERS=OFF \
    -D FORCE_VTK=OFF \
    -D WITH_IPP=NO \
    -D WITH_1394=NO \
    -D WITH_LIBV4L=NO \
    -D WITH_V4l=YES \
    -D WITH_TBB=YES \
    -D WITH_FFMPEG=YES \
    -D WITH_GPHOTO2=YES \
    -D WITH_GSTREAMER=YES \
    -D WITH_GDAL=OFF \ 
    -D WITH_OPENEXR=OFF \
    -D WITH_OPENGL=OFF \ 
    -D WITH_GTK=ON \
    -D WITH_QT=NO \
    -D WITH_XINE=OFF \ 
    -D BUILD_JPEG=ON  \
    -D BUILD_TIFF=ON \
    -D BUILD_PNG=ON \
    -D PYTHON3_LIBRARY=`find /usr -name libpython3.so` \
    -D PYTHON3_EXECUTABLE=`which python3` \
    -D PYTHON2_LIBRARY=`find /usr -name libpython2.so` \
    -D PYTHON2_EXECUTABLE=`which python2` \
     .. && \
  make -j$(nproc) && \
  make install && \
  rm -rf /opt/opencv-${OPENCV_VERSION} && \
  ln -vfs /usr/local/lib64/pkgconfig/opencv4.pc /usr/lib/pkgconfig/opencv4.pc && \
  ln -vfs /usr/local/include/opencv4/opencv2 /usr/local/include/opencv2

ENV PKG_CONFIG_PATH=/usr/local/lib64/pkgconfig:/usr/lib/pkgconfig

RUN mkdir -p /projects

WORKDIR /projects

# Command to compile
# g++ -Bstatic -static-libgcc -std=c++11 app.cpp -o app $(pkg-config --cflags --libs -static opencv4) -lgfortran -lquadmath
