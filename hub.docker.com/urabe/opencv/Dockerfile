FROM urabe/opencv:base_cpu

MAINTAINER Kazuki Urabe <urabe0225@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
WORKDIR /opt/

RUN cd /opt/opencv && git checkout refs/tags/3.3.1 && \
    cd /opt/opencv_contrib && git checkout refs/tags/3.3.1

RUN mkdir /opt/opencv/build && cd /opt/opencv/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=ON \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D OPENCV_EXTRA_MODULES_PATH=/opt/opencv_contrib/modules \
    -D WITH_TBB=ON \
    -D BUILD_EXAMPLES=ON .. && \
    make -j$(nproc) && make install
