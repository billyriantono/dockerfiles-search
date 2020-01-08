FROM centos:7

RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7

RUN yum update -y
RUN yum install -y centos-release-scl

RUN yum install -y \
    nano \
    wget \
    pygpgme \
    git \
    unzip \
    gcc-c++ \
    make

# Dev tools
RUN yum groupinstall "Development Tools" -y && \
    yum install -y curl-devel zlib-devel libssl-dev centos-release-scl makecache devtoolset-7-gcc devtoolset-7-gcc-c++ && \
    wget https://cmake.org/files/v3.6/cmake-3.6.2.tar.gz && \
    tar -zxvf cmake-3.6.2.tar.gz && \
    rm cmake-3.6.2.tar.gz && \
    cd cmake-3.6.2 && \
    ./bootstrap --prefix=/usr/local --system-curl && \
    make && \
    make install && \
    cd .. && \
    rm -R cmake-3.6.2

# Dl opencv
RUN wget https://github.com/opencv/opencv_contrib/archive/4.1.1.zip && \
    unzip 4.1.1.zip && \
    rm 4.1.1.zip && \
    wget https://github.com/opencv/opencv/archive/4.1.1.zip && \
    unzip 4.1.1.zip && \
    rm 4.1.1.zip

# Conf build & conf opencv
RUN export PKG_CONFIG=/usr/bin/pkg-config && export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib64/pkgconfig/ && export LD_LIBRARY_PATH="/usr/local/lib64/" && \
    cd opencv-4.1.1 && \
    mkdir build && \
    cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_TBB=ON \
          -D WITH_V4L=ON \
          -D INSTALL_C_EXAMPLES=OFF \
          -D INSTALL_PYTHON_EXAMPLES=OFF \
          -D BUILD_EXAMPLES=OFF \
          -D BUILD_JAVA=OFF \
          -D BUILD_TESTS=OFF \
          -D WITH_QT=OFF \
          -D WITH_OPENGL=ON \
          -D BUILD_opencv_world=ON \
          -D OPENCV_PYTHON_SKIP_DETECTION=ON \
          -D OPENCV_GENERATE_PKGCONFIG=ON \
          -D OPENCV_PC_FILE_NAME=opencv4.pc \
          -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.1.1/modules .. && \
    make && \
    make install && \
    cd ../.. && \
    rm -R opencv-4.1.1 && \
    rm -R opencv_contrib-4.1.1 && \
    echo '/usr/local/lib64/' >> /etc/ld.so.conf.d/opencv.conf && \
    ldconfig

# Cleaning
RUN yum remove -y gcc-c++ make cmake gcc && yum clean all && yum -y autoremove

# prepare dir
RUN mkdir /source

VOLUME ["/source"]
WORKDIR /source
CMD ["bash"]