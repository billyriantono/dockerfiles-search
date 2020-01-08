FROM ubuntu:latest

#developer tools
RUN apt-get -y update && apt-get -y install build-essential cmake pkg-config git

#opencv prerequites
RUN apt-get -y install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev \
	libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev \
	libgtk-3-dev libatlas-base-dev gfortran

#python
RUN apt-get -y install python-dev python3-dev python3-pip && pip3 install numpy scipy matplotlib scikit-image scikit-learn ipython

#opencv
RUN mkdir work && cd work && git clone https://github.com/opencv/opencv.git \
	&& git clone https://github.com/opencv/opencv_contrib.git 
RUN cd work/opencv && mkdir build && cd build && cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
    -D PYTHON3_EXECUTABLE=/usr/bin/python3 \
    -D PYTHON3_PACKAGES_PATH=/usr/lib/python3.5/site-packages \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D BUILD_EXAMPLES=ON ..
RUN cd work/opencv/build make -j 4 && make install
RUN mv /usr/lib/python3.5/site-packages/cv2.cpython-35m-x86_64-linux-gnu.so /usr/lib/python3.5/site-packages/cv2.so
