FROM ubuntu:16.04

RUN apt-get update

RUN apt-get install -y build-essential cmake git pkg-config
RUN apt-get install -y libjpeg-dev libtiff-dev libjasper-dev libpng-dev
RUN apt-get install -y libgtk2.0-dev
RUN apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
RUN apt-get install -y libatlas-base-dev gfortran
RUN apt-get install -y python-dev python-pip

RUN pip install numpy 

RUN cd ~ && \
git clone https://github.com/Itseez/opencv.git && \
git clone https://github.com/Itseez/opencv_contrib.git && \
#cd ~/opencv && git checkout 3.4.5 && \
#cd ~/opencv_contrib && git checkout 3.4.5 && \
mkdir ~/opencv/build && cd ~/opencv/build && \
cmake -D CMAKE_BUILD_TYPE=Release -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules -D CMAKE_INSTALL_PREFIX=/usr/local .. && \
make -j5 && \
make install && \
ldconfig && \
cd ~ && rm -rf opencv opencv_contrib

#RUN apt-get install -y tesseract-ocr libtesseract-dev libleptonica-dev
#RUN apt-get install -y bc imagemagick

#RUN pip install pytesseract xlsxwriter pdf2image

#RUN cd ~ && \
#git clone https://github.com/brian-yang/table-parser-opencv.git

