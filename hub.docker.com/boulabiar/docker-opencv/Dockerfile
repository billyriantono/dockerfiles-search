FROM ubuntu:16.04

MAINTAINER Alexey Kornilov <alexey.kornilov@kavolorn.ru>

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y unzip wget build-essential \
		cmake git pkg-config libswscale-dev \
		python3-dev python3-numpy \
		libtbb2 libtbb-dev libjpeg-dev \
		libpng-dev libtiff-dev libjasper-dev \
        ipython python3-pip python3-pil \
        python3-matplotlib python3-scipy \
        tesseract-ocr tesseract-ocr-dan \
        tesseract-ocr-eng libtesseract3

RUN pip3 install pytesseract

RUN cd \
	&& wget https://github.com/opencv/opencv/archive/3.3.0.zip \
	&& unzip 3.3.0.zip \
	&& cd opencv-3.3.0 \
	&& mkdir build \
	&& cd build \
	&& cmake .. \
	&& make -j3 \
	&& make install \
	&& cd \
	&& rm 3.3.0.zip
