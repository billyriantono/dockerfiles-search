FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu16.04

RUN apt-get update && apt-get install -y \
		build-essential \
		cmake \
		curl \
		git


RUN apt-get update && apt-get install -y \
		libffi-dev \
		libfreetype6-dev \
		libhdf5-dev \
		libjpeg-dev \
		liblcms2-dev \
		libopenblas-dev \
		liblapack-dev \
		libopenjpeg5 \
		libpng12-dev

RUN apt-get update && apt-get install -y \
		software-properties-common

RUN add-apt-repository ppa:jonathonf/python-3.6 -y && apt update -y && apt install python3.6 -y
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1

ENV PYTHON_VERSION 3.6.5

RUN apt-get update && apt-get install -y \
		pkg-config \
		unzip \
		vim \
		wget \
		zlib1g-dev \
		libjpeg-dev \
		libpng-dev \
		libtiff5-dev \
		libjasper-dev \
		libopenexr-dev \
		libgdal-dev \
		libdc1394-22-dev \
		libavcodec-dev \
		libavformat-dev \
		libswscale-dev
RUN apt-get update && apt-get install -y \
		libtheora-dev \
		libvorbis-dev \
		libxvidcore-dev \
		libx264-dev \
		yasm \
		libopencore-amrnb-dev \
		libopencore-amrwb-dev \
		libv4l-dev \
		libxine2-dev \
		libtbb-dev \
		libeigen3-dev

RUN apt-get update
RUN apt-get install -y python3-requests
RUN apt-get install -y default-jdk &&\
     rm -rf /var/lib/apt/lists/*

RUN cd ~ &&\
    git clone https://github.com/Itseez/opencv.git &&\
    wget http://sourceforge.net/projects/opencvlibrary/files/opencv-unix/2.4.9/opencv-2.4.9.zip &&\
    unzip opencv-2.4.9.zip &&\
    cd opencv-2.4.9 &&\
    mkdir build && cd build &&\
    cmake -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_IPP=OFF -D CMAKE_INSTALL_PREFIX=/usr .. &&\
    make &&\
    make install &&\
    cd ~ &&\
    rm -rf opencv opencv-2.4.9 opencv-2.4.9.zip


# Install pip
RUN apt-get update && apt-get install -y python3-pip
RUN pip3 install --upgrade pip

RUN apt-get update && apt-get install -y libgoogle-glog-dev libatlas-base-dev
RUN apt-get install -y libspqr2.0.2
RUN apt-get install -y libcxsparse3.1.4
RUN apt-get install -y libboost-python-dev
RUN apt-get install -y libpython3.6-dev
RUN apt-get install libcgal-dev -y



# Install useful Python packages using apt-get to avoid version incompatibilities with Tensorflow binary
# especially numpy, scipy, skimage and sklearn (see https://github.com/tensorflow/tensorflow/issues/2034)
RUN apt-get update && \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*


WORKDIR "/var/app/"
