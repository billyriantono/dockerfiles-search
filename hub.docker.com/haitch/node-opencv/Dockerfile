FROM node

RUN echo 'deb http://archive.ubuntu.com/ubuntu trusty multiverse' >> /etc/apt/sources.list 

RUN apt-get update
RUN apt-get install -y --force-yes wget libjpeg-dev zlibc libwebp-dev libtiff-dev
RUN apt-get install -y --force-yes libopencv-dev
#RUN ln /dev/null /dev/raw1394