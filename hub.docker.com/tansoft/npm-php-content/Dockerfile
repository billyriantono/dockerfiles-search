FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

# nvidia-container-runtime (for Linux users)
#ENV NVIDIA_VISIBLE_DEVICES \
#    ${NVIDIA_VISIBLE_DEVICES:-all}
#ENV NVIDIA_DRIVER_CAPABILITIES \
#    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

ENV USER_NAME="dev"

RUN apt-get update && apt-get install -y \
            wget \
            vim \
            gosu \
            unzip \
            cmake \
            apt-utils \
            python3-dev \
            python3-pip

########################            
# open cv installation #
########################
ENV OPENCV_VER="3.4.6"

RUN apt-get install -y libjpeg-dev libpng-dev libtiff-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libgtk-3-dev
RUN pip3 install numpy

WORKDIR /tmp/
RUN wget -O opencv.zip https://github.com/opencv/opencv/archive/$OPENCV_VER.zip
RUN wget -O opencv_contrib.zip https://github.com/opencv/opencv_contrib/archive/$OPENCV_VER.zip
RUN unzip opencv.zip
RUN unzip opencv_contrib.zip
WORKDIR opencv-$OPENCV_VER
RUN mkdir build 
WORKDIR ./build
RUN cmake -D CMAKE_BUILD_TYPE=Release \
          -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D PYTHON_EXECUTABLE=$(which python) \
          -D BUILD_EXAMPLES=ON \
          -D INSTALL_PYTHON_EXAMPLES=ON \
          -D OPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib-$OPENCV_VER/modules \
          ..
RUN make -j4
RUN make install
RUN rm -rf /tmp/*

########################


##########################       
# open pose installation #
##########################
ENV OPENPOSE_VER="1.5.0"

RUN DEBIAN_FRONTEND=noninteractive apt install -y caffe-cuda
RUN apt install -y libprotobuf-dev protobuf-compiler libgoogle-glog-dev libboost-all-dev libcaffe-cuda-dev libhdf5-dev libatlas-base-dev

WORKDIR /tmp/

RUN wget -O openpose.zip https://github.com/CMU-Perceptual-Computing-Lab/openpose/archive/v$OPENPOSE_VER.zip
RUN unzip openpose.zip
RUN mv openpose-* openpose
RUN mkdir -p ./openpose/build && cd ./openpose/build && \
    cmake -DCaffe_INCLUDE_DIRS=/usr/include/caffe \ 
          -DCaffe_LIBS=/usr/lib/x86_64-linux-gnu/libcaffe.so \
          -DBUILD_CAFFE=OFF .. && \
    make -j`nproc` && make install

##########################


RUN rm -rf /var/lib/apt/lists/*

# set password for root user
RUN echo "root:root" | chpasswd

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]
