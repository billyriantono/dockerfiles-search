FROM nvidia/cuda:9.0-cudnn7-devel
LABEL maintainer "Abhishek Maharjan <rpidanny.abhishek@gmail.com>"

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3-pip \
  tmux \
  zsh \
  curl \
  git \
  wget \
  nano \
  locales \
  libgtk2.0-dev

RUN locale-gen en_US.UTF-8 && update-locale LANG=en_US.UTF-8

RUN pip3 install -U pip

RUN pip install tensorflow-gpu===1.10.0 opencv-python==3.4.2.17 pillow h5py scipy colorama
