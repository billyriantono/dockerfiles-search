FROM tensorflow/tensorflow:1.12.0-gpu-py3
MAINTAINER watai <t.watai@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    language-pack-ja \
    wget \
    vim \
    git \
    unzip \
    zip \
    cmake \
    libgtk2.0-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# locale setting
RUN locale-gen ja_JP.UTF-8
ENV LANGUAGE ja_JP:en
ENV LC_ALL ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
RUN update-locale LANG=$LANG

# install opencv3
ARG OPENCV_VERSION=3.4.4
WORKDIR /root
ENV PYTHON_INCLUDE_DIRS /usr/include/python3.5
ENV PYTHON_LIBRARIES /usr/lib/x86_64-linux-gnu/libpython3.5m.so
RUN wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip && \
    unzip ${OPENCV_VERSION}.zip -d . && \
    mkdir -p opencv-${OPENCV_VERSION}/build && \
    rm ${OPENCV_VERSION}.zip
RUN wget https://github.com/opencv/opencv_contrib/archive/${OPENCV_VERSION}.zip && \
    unzip ${OPENCV_VERSION}.zip && \
    rm ${OPENCV_VERSION}.zip
RUN cd opencv-${OPENCV_VERSION}/build \
    && cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib-${OPENCV_VERSION}/modules \
    -D BUILD_opencv_java=OFF \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D WITH_TBB=OFF \
    -D WITH_QT=OFF \
    -D WITH_1394=OFF \
    -D WITH_CUDA=OFF .. \
    && make -j8 \
    && make install \
    && make clean \
    && ldconfig \
    && ln /dev/null /dev/raw1394 \
    && rm -r /root/opencv-${OPENCV_VERSION} /root/opencv_contrib-${OPENCV_VERSION}

# install python modules
RUN pip install --upgrade \
    pip \
    opencv-python

# matplotlib font setting
RUN apt-get update && \
    apt-get install -y fonts-ipaexfont && \
    mkdir -p /root/.config/matplotlib && \
    cp /usr/local/lib/python3.5/dist-packages/matplotlib/mpl-data/matplotlibrc /root/.config/matplotlib/matplotlibrc && \
    echo font.family : IPAexGothic >> /root/.config/matplotlib/matplotlibrc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /notebooks
