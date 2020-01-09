FROM ubuntu:xenial

# install dependencies
RUN apt-get update && apt-get install -y \
qtbase5-dev \
libxt-dev \
libqt5x11extras5-dev \
libqt5webkit5-dev \
cmake-curses-gui \
libboost1.58-all-dev \
libflann-dev \
libeigen3-dev \
cmake \
build-essential \
git --no-install-recommends \

# install vtk and opencv dependencies
libvtk6-dev \
libvtk6-qt-dev \
libproj-dev \
libgtk2.0-dev \
python-dev \
python-numpy \
libtbb2 \
libtbb-dev \
libdc1394-22-dev \
python2.7-dev \
python-pip \
&& pip install --upgrade pip \
&& pip install numpy \
&& apt-get autoclean && apt-get clean \
&& rm -rf /var/lib/apt/lists/*

# install opencv
RUN \
cd ~ && \
git clone -b 2.4 https://github.com/opencv/opencv.git && \
cd opencv && \
pwd && \

#cd ~ && \
#git clone https://github.com/Itseez/opencv_contrib.git && \
#cd opencv_contrib && \
#git checkout 3.1.0 && \

cd /root/opencv && \
mkdir build && \
cd build && \
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_C_EXAMPLES=OFF \
-D INSTALL_PYTHON_EXAMPLES=ON \
#-D OPENCV_EXTRA_MODULES_PATH=/root/opencv_contrib/modules \
#-D BUILD_EXAMPLES=ON 
.. && \

cd ~/opencv/build && \
make -j $(nproc) && \
make install && \
ldconfig && \

cp ~/opencv/build/lib/cv2.so /usr/local/lib/python2.7/dist-packages/ && \
cd ~ && rm -rf ./*
# step 11
# RUN cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
# RUN ln -s /usr/local/lib/python2.7/site-packages/cv2.so cv2.so
