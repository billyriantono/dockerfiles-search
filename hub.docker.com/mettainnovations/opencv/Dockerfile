FROM mettainnovations/ubuntu-base:16.04

RUN mkdir -p /home/developer
ENV HOME /home/developer
WORKDIR /home/developer

# Download and Install OpenCV
RUN git clone https://github.com/opencv/opencv_contrib.git && \
    cd opencv_contrib && \
    git checkout 3.4.4 && \
    cd .. && \
    git clone https://github.com/opencv/opencv.git && \
    cd opencv && \
    git checkout 3.4.4 && \
    git submodule init && \
    git submodule update && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF -DWITH_QT=YES -DWITH_OPENMP=YES -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -DCMAKE_CXX_FLAGS="-Wno-deprecated-declarations" .. && \
    make -j4 && \
    make install 
