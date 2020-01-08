FROM tensorflow/tensorflow:1.12.0-gpu-py3
RUN apt-get update
RUN apt-get install -y language-pack-ja-base language-pack-ja libopencv-dev python-opencv
ENV LANG ja_JP.UTF-8
RUN pip --no-cache-dir install keras
RUN pip3 install opencv-python
