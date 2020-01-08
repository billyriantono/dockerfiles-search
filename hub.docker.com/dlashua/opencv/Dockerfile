FROM python:3.7-alpine

ENV OPENCV_VERSION 4.1.0
RUN apk --no-cache --update-cache add build-base git gtk+2.0-dev ffmpeg-dev gst-plugins-base-dev cmake \
  && pip install numpy==1.16.2 \
  && git clone https://github.com/opencv/opencv.git \
  && cd opencv \
  && git checkout ${OPENCV_VERSION} \
  && mkdir build \
  && cd build \
  && cmake ../ \
  && make \
  && make install \
  && cd ../../ \
  && rm -rf opencv


