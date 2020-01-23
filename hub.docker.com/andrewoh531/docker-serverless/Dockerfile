FROM ubuntu:16.04
MAINTAINER Andrew Demchenko "a.demchenko@quantumobile.com"

ARG OPENCV_VERSION="3.1.0"

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install build-essential cmake pkg-config -y
RUN apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev -y
RUN apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev -y
RUN apt-get install libxvidcore-dev libx264-dev -y
RUN apt-get install libgtk-3-dev -y
RUN apt-get install libatlas-base-dev gfortran -y
RUN apt-get install python2.7-dev python3.5-dev -y
RUN apt-get install wget unzip -y

RUN ln /dev/null /dev/raw1394

RUN wget -O opencv.zip https://github.com/Itseez/opencv/archive/$OPENCV_VERSION.zip
RUN unzip opencv.zip
RUN wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/$OPENCV_VERSION.zip
RUN unzip opencv_contrib.zip

RUN apt-get install python-pip -y
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

WORKDIR /opencv-$OPENCV_VERSION/
RUN mkdir build
WORKDIR build
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib-$OPENCV_VERSION/modules \
    -D PYTHON_EXECUTABLE=/usr/bin/python \
    -D BUILD_EXAMPLES=ON /opencv-$OPENCV_VERSION/

RUN make clean
RUN make
RUN make install

RUN ldconfig

CMD ["bash"]