FROM ubuntu:14.04
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y wget unzip build-essential git cmake pkg-config libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libgtk2.0-dev libatlas-base-dev gfortran
RUN apt-get install -y python2.7-dev
RUN wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.0.0.zip && unzip opencv.zip
RUN wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py && pip install numpy
RUN cd opencv-3.0.0/ && mkdir build && cd build && cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=OFF -D INSTALL_PYTHON_EXAMPLES=OFF -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.0.0/modules -D BUILD_opencv_gpu=OFF -D BUILD_EXAMPLES=ON .. && make && make install && ldconfig && cd ../../ && rm opencv.zip && rm -rf opencv-3.0.0
