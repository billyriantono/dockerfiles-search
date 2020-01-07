FROM tensorflow/tensorflow:1.10.1-gpu-py3
MAINTAINER Wonkyung Lee <leewk921223@gmail.com>

RUN apt-get update
RUN apt-get install -y \
    git\
    vim \
    zsh \
    tmux

# Install language pack
RUN apt-get install -y \
    language-pack-en
RUN locale-gen en_US.utf8
RUN update-locale
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

RUN curl -fsSL https://dotfiles.wook.kr/etc/install | bash

# Install python packages for image processing.
RUN pip3 install scikit-image
RUN pip3 install opencv-python
RUN apt install -y libsm6 libxext6 libxrender-dev
RUN pip3 install cmake
RUN pip3 install dlib

CMD ["zsh"]
