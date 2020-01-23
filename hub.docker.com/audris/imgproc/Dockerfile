FROM python:3.6

MAINTAINER Audris Mockus <audris@mockus.org>

USER root

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
RUN echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.6 main" | tee /etc/apt/sources.list.d/mongodb-org-3.6.list


RUN apt-get update && \
    apt-get install -y \
    libopenblas-base \
    openssh-server \
    lsof sudo \
    sssd \
    sssd-tools \
    vim \
    git \
    curl lsb-release \
    tmux  zsh zip build-essential \
    python3-dev \
    ipython3 \
    ipython3-notebook \
    python3-tk \
    python3-pip \
	 imagemagick \
	 build-essential \
	 cmake \
	 git \
	 wget \
	 unzip \
	 yasm \
	 pkg-config \
	 libswscale-dev \
	 libtbb2 \
	 libtbb-dev \
	 libjpeg-dev \
	 libpng-dev \
	 libtiff-dev \
	 libjasper-dev \
	 libavformat-dev \
	 libpq-dev \
	 libboost-all-dev \
	 mongodb-org-shell \
	 mongodb-org-tools
	 


RUN pip3 install --upgrade pip
RUN pip3 install Pillow numpy 

ENV LC_ALL=C

WORKDIR /
RUN wget https://github.com/Itseez/opencv/archive/3.2.0.zip \
&& unzip 3.2.0.zip \
&& mkdir /opencv-3.2.0/cmake_binary \
&& cd /opencv-3.2.0/cmake_binary \
&& cmake -DBUILD_TIFF=ON \
 -DBUILD_opencv_java=OFF \
 -DWITH_CUDA=OFF \
 -DENABLE_AVX=ON \  
 -DWITH_OPENGL=ON \
 -DWITH_OPENCL=ON \
 -DWITH_IPP=ON \
 -DWITH_TBB=ON \
 -DWITH_EIGEN=ON \
 -DWITH_V4L=ON \
 -DBUILD_TESTS=OFF \
 -DBUILD_PERF_TESTS=OFF \
 -DCMAKE_BUILD_TYPE=RELEASE \
 -DCMAKE_INSTALL_PREFIX=$(python3.6 -c "import sys; print(sys.prefix)") \
 -DPYTHON_EXECUTABLE=$(which python3.6) \
 -DPYTHON_INCLUDE_DIR=$(python3.6 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
 -DPYTHON_PACKAGES_PATH=$(python3.6 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") .. \
&& make install \
&& rm /3.2.0.zip \
&& rm -r /opencv-3.2.0

RUN pip install flake8 pep8 --upgrade

COPY eecsCA_v3.crt /etc/ssl/ 
COPY sssd.conf /etc/sssd/ 
COPY common* /etc/pam.d/ 
RUN chmod 0600 /etc/sssd/sssd.conf /etc/pam.d/common* 
RUN if [ ! -d /var/run/sshd ]; then mkdir /var/run/sshd; chmod 0755 /var/run/sshd; fi

COPY cropTag init.sh startsvc.sh startshell.sh notebook.sh startDef.sh /bin/ 

ENV NB_USER jovyan
ENV NB_UID 1000
ENV HOME /home/$NB_USER
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && mkdir $HOME/.ssh && chown -R $NB_USER:users $HOME 
RUN chown -R $NB_USER:users $HOME && chmod -R og-rwx $HOME/.ssh
