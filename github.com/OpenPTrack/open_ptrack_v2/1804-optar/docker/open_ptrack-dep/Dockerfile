FROM nvidia/opengl:1.0-glvnd-runtime-ubuntu18.04

LABEL maintainer "Samir Tabriz"

ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES},display,compute,utility

RUN apt-get update \ 
    && apt-get install -y --no-install-recommends mesa-utils \ 
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update \ 
    && apt-get install -y --no-install-recommends         ocl-icd-libopencl1         clinfo \ 
    &&     rm -rf /var/lib/apt/lists/*
    
RUN mkdir -p /etc/OpenCL/vendors \ 
    && echo "libnvidia-opencl.so.1" > /etc/OpenCL/vendors/nvidia.icd

ENV NVIDIA_VISIBLE_DEVICES=all

RUN  echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections     \ 
    && echo keyboard-configuration keyboard-configuration/layout select 'English (US)' | debconf-set-selections     \ 
    && echo keyboard-configuration keyboard-configuration/layoutcode select 'us' | debconf-set-selections     \ 
    && apt-get update     \ 
    && apt-get install -y --no-install-recommends software-properties-common wget udev apt-utils sudo 

RUN  add-apt-repository -y ppa:danielrichter2007/grub-customizer     \ 
    && apt-get install -y apt-transport-https     \ 
    && apt-add-repository -y ppa:obsproject/obs-studio     \ 
    && apt-add-repository -y ppa:graphics-drivers/ppa     \ 
    && add-apt-repository -y ppa:yannubuntu/boot-repair     \ 
    && apt-get update     \ 
    && apt-get install -y grub-customizer exfat-fuse exfat-utils vim terminator gitg cmake-curses-gui gparted meld cowsay fortune gimp synaptic libgoogle-glog-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev ncdu filezilla p7zip-full openssh-client openssh-server boot-repair   \
    && ln -s /usr/lib/x86_64-linux-gnu/lapack/liblapack.so.3.7.1 /usr/lib/liblapack.so.3

RUN  sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'     \ 
    && apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654     \ 
    && apt-get update     \ 
    && apt-get install ros-melodic-desktop-full python-rosinstall -y     \ 
    && rosdep init     \ 
    && rosdep update         

RUN  /bin/bash -c "echo 'source /opt/ros/melodic/setup.bash' >> /root/.bashrc \ 
    && source /root/.bashrc"      

RUN  /bin/bash -c "source /opt/ros/melodic/setup.bash     \ 
    && cd     \ 
    && mkdir -p workspace/ros/src     \ 
    && cd workspace/ros     \ 
    && catkin_make"     

RUN  /bin/bash -c "echo 'source /root/workspace/ros/devel/setup.bash' >> /root/.bashrc"          

RUN  cd ~/workspace/ros     \ 
    && apt-get install -y ocl-icd-opencl-dev     \ 
    && wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda_10.0.130_410.48_linux -O cuda.run     \ 
    && chmod +x cuda.run     \ 
    && ./cuda.run -silent --toolkit --samples --samplespath="/root/workspace/"     \ 
    && wget http://openptrack.org/dl/cudnn-10.0-linux-x64-v7.3.1.20.tgz     \ 
    && tar -zxvf cudnn*     \
    && cp cuda/include/* /usr/local/cuda/include     \ 
    && cp cuda/lib64/* /usr/local/cuda/lib64/     \ 
    && echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64' >> ~/.bashrc     \ 
    && echo 'export PATH=$PATH:/usr/local/cuda/bin' >> ~/.bashrc          
    
RUN  apt-get install cmake libgoogle-glog-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev -y --force-yes     \ 
    && mkdir /tmp/ceres_install     \ 
    && cd /tmp/ceres_install     \ 
    && git clone https://ceres-solver.googlesource.com/ceres-solver     \ 
    && cd ceres-solver     \ 
    && git fetch --tags     \ 
    && git checkout tags/1.12.0     \ 
    && cd ..     \ 
    && mkdir ceres-bin     \ 
    && cd ceres-bin     \ 
    && cmake ../ceres-solver     \ 
    && make -j8     \ 
    && make test     \ 
    && make install     \ 
    && rm -R /tmp/ceres_install     \ 
    && cd ~/workspace/ros/src     \ 
    && git clone https://github.com/iaslab-unipd/calibration_toolkit     \ 
    && cd calibration_toolkit     \ 
    && git fetch origin --tags     \ 
    && git checkout tags/v0.2         

RUN  /bin/bash -c "source /root/.bashrc    \ 
    && cd ~/workspace/ros/src      \ 
    && git clone https://bitbucket.org/mcarraro/rtpose_wrapper     \ 
    && cd rtpose_wrapper     \ 
    && git checkout integration-1604     \ 
    && sed -i -e 's/CUDNN_CROSS_CORRELATION/CUDNN_CROSS_CORRELATION, CUDNN_DATA_FLOAT/g' include/caffe/util/cudnn.hpp   \
    && apt-get --assume-yes install libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler libboost-all-dev libgflags-dev libgoogle-glog-dev liblmdb-dev    \
    && make all -j8"

RUN  cd     \ 
    && cd workspace     \ 
    && git clone https://github.com/OpenPTrack/libfreenect2.git     \ 
    && cd libfreenect2     \ 
    && git checkout 1606     \ 
    && cd depends/     \ 
    && apt-get update     \ 
    && apt-get install -y git cmake cmake-curses-gui libxmu-dev libxi-dev libgl1-mesa-dev xorg-dev libglu1-mesa-dev libtool automake libudev-dev libgtk2.0-dev pkg-config libjpeg-turbo8-dev libturbojpeg libglewmx-dev libturbojpeg0-dev     \ 
    && ln -f -s /usr/lib/x86_64-linux-gnu/libturbojpeg.so.0.1.0 /usr/lib/x86_64-linux-gnu/libturbojpeg.so     \ 
    && cd .. \
    && mkdir build \ 
    && cd build     \ 
    && /bin/bash -c "cmake .. -DENABLE_CXX11=ON -DCUDA_PROPAGATE_HOST_FLAGS=off   \ 
    && make     \
    && make install"     \
    && echo '# ATTR{product}=="Kinect2" SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02c4", MODE="0666" SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02d8", MODE="0666" SUBSYSTEM=="usb", ATTR{idVendor}=="045e", ATTR{idProduct}=="02d9", MODE="0666"' > ~/90-kinect2.rules     \ 
    && cp ~/90-kinect2.rules /etc/udev/rules.d/

RUN  cd ~/workspace/ros/src     \ 
    && git clone https://github.com/OpenPTrack/iai_kinect2.git     \ 
    && cd iai_kinect2     \ 
    && git checkout 1607       


RUN  /bin/bash -c "git clone https://github.com/nagadomi/distro.git ~/torch --recursive \ 
    && cd ~/torch \ 
    && bash install-deps \ 
    && ./install.sh -b \ 
    && source ~/.bashrc \ 
    && cd install/bin \ 
    && ./luarocks install dpnn \ 
    && ./luarocks install csvigo"

RUN /bin/bash -c "cd /tmp \
    && git clone https://github.com/cmusatyalab/openface.git \
    && cd openface \
    && sudo python setup.py install"

RUN /bin/bash -c "cd /tmp \
    && rm -rf dlib \
    && git clone https://github.com/davisking/dlib.git \
    && cd dlib \
    && git checkout v19.4 \
    && mkdir python_examples/build \
    && cd python_examples/build \
    && cmake ../../tools/python -DUSE_AVX_INSTRUCTIONS=ON \
    && cmake --build . --config Release \
    && sudo cp dlib.so /usr/local/lib/python2.7/dist-packages"

RUN apt-get update \
    && apt-get install -y python-qt4 python-pip \
    && pip install requests

RUN apt-get install ntp -y  \ 
    && rm -rf /var/lib/apt/lists/*