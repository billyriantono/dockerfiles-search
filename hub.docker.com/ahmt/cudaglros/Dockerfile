#  THIS CUDA + OPENGL IMAGE
FROM nvidia/cudagl:9.0-devel-ubuntu16.04

WORKDIR /root/
# Install build dependencies
RUN apt-get update && apt-get install -y \
    libsqlite3-dev \
    libpcl-dev \
    git \
    cmake \
    libproj-dev \
    libqt5svg5-dev \
    libfreenect-dev \
    libopenni2-dev \
    libyaml-cpp-dev \
    libpcap0.8-dev \
    software-properties-common \
    libgtk2.0-dev \
    pkg-config \
    sudo \
    apt-utils \
    tree \
    vim

#RUN apt-get update && apt-get install -y --no-install-recommends \
#        cuda-core-$CUDA_PKG_VERSION \
#        cuda-misc-headers-$CUDA_PKG_VERSION \
#        cuda-command-line-tools-$CUDA_PKG_VERSION \
#        cuda-nvrtc-dev-$CUDA_PKG_VERSION \
#        cuda-nvml-dev-$CUDA_PKG_VERSION \
#        cuda-nvgraph-dev-$CUDA_PKG_VERSION \
#        cuda-cusolver-dev-$CUDA_PKG_VERSION \
#        cuda-cublas-dev-8-0=8.0.61.2-1 \
#        cuda-cufft-dev-$CUDA_PKG_VERSION \
#        cuda-curand-dev-$CUDA_PKG_VERSION \
#        cuda-cusparse-dev-$CUDA_PKG_VERSION \
#        cuda-npp-dev-$CUDA_PKG_VERSION \
#        cuda-cudart-dev-$CUDA_PKG_VERSION \
#        cuda-driver-dev-$CUDA_PKG_VERSION && \
#        rm -rf /var/lib/apt/lists/* ENV LIBRARY_PATH /usr/local/cuda/lib64/stub


#FROM ubuntu:16.04

# # OpenCV  version <= 3.1.0
# RUN git clone https://github.com/opencv/opencv_contrib.git
# RUN git clone https://github.com/opencv/opencv.git
# RUN cd opencv_contrib && \
#     git checkout tags/3.1.0 && \
#     cd && \
#     cd opencv && \
#     git checkout tags/3.1.0 && \
#     mkdir build && \
#     cd build && \
#     cmake -DOPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib/modules -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF .. && \
#     make -j4 && \
#     make install && \
#     cd && \
#     rm -rf opencv opencv_contrib
#

#pengl fix
#COPY --from= nvidia/opengl:1.1-glvnd-devel-ubuntu16.04 \
#          /usr/local/lib/x86_64-linux-gnu \
#          /usr/local/lib/x86_64-linux-gnu
#
#COPY --from= nvidia/opengl:1.1-glvnd-devel-ubuntu16.04 \
#          /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json \
#          /usr/local/share/glvnd/egl_vendor.d/10_nvidia.json
#
RUN echo '/usr/local/lib/x86_64-linux-gnu' >> /etc/ld.so.conf.d/glvnd.conf && \
          ldconfig && \
          echo '/usr/local/$LIB/libGL.so.1' >> /etc/ld.so.preload && \
          echo '/usr/local/$LIB/libEGL.so.1' >> /etc/ld.so.preload


# Install ROS to build other odometry approaches (depending on ROS)
# install packages
RUN apt-get update && apt-get install -q -y \
    dirmngr \
    gnupg2 \
    gnupg \
    lsb-release \
    && rm -rf /var/lib/apt/lists/*

# setup keys
#RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 421C365BD9FF1F717815A3895523BAEEB01FA116
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list


# install bootstrap tools
RUN apt-get update && apt-get install --no-install-recommends -y \
    python-rosdep \
    python-rosinstall \
    python-vcstools \
    && rm -rf /var/lib/apt/lists/*

# setup environment
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# bootstrap rosdep
RUN rosdep init \
    && rosdep update

# install ros packages
ENV ROS_DISTRO kinetic
RUN apt-get update && apt-get install -y \
    ros-kinetic-desktop-full \
    && rm -rf /var/lib/apt/lists/*




## install ROS dependencies
#RUN apt-get update && apt-get install -y ros-kinetic-tf ros-kinetic-pcl-ros ros-kinetic-eigen-conversions ros-kinetic-tf-conversions ros-kinetic-random-numbers ros-kinetic-image-transport libblas-dev liblapack-dev libsuitesparse-dev libvtk6.2 libyaml-cpp-dev wget libgoogle-glog-dev libatlas-base-dev ros-kinetic-sophus ros-kinetic-octomap libglew-dev ros-kinetic-cv-bridge ros-kinetic-vision-opencv ros-kinetic-velodyne ros-kinetic-roslint
#
##RUN apt-get update && apt-get install -y ros-kinetic-velodyne
#
#
## # GTSAM
## RUN git clone https://bitbucket.org/gtborg/gtsam.git
## RUN cd gtsam && \
##     git checkout 4.0.0-alpha2 && \
##     mkdir build && \
##     cd build && \
##     cmake -DMETIS_SHARED=ON -DGTSAM_BUILD_STATIC_LIBRARY=OFF -DGTSAM_USE_SYSTEM_EIGEN=ON -DGTSAM_BUILD_TESTS=OFF -DGTSAM_BUILD_EXAMPLES_ALWAYS=OFF -DCMAKE_BUILD_TYPE=Release .. && \
##     make -j3 && \
##     make install && \
##     cd && \
##     rm -r gtsam
#
#
## Run installers.
##COPY installers /tmp/installers
##RUN bash /tmp/installers/pre_install.sh
#

WORKDIR /root
