FROM ubuntu:14.04

MAINTAINER Toshiaki Inahata <darwin49@gmail.com>

# TensorFlow Binary URL
ENV TF_BINARY_URL https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0rc0-cp27-none-linux_x86_64.whl

#
# Set UP Ubuntu
#
RUN sudo apt-get update
RUN sudo apt-get upgrade -y

#
# Install Python
#
RUN sudo apt-get install -y python-pip python-dev
RUN sudo pip install --upgrade pip

#
# Install Libraries
#
RUN sudo pip install Pillow
RUN sudo pip install --upgrade ${TF_BINARY_URL}

#
# Install OpenCV
#
RUN sudo apt-get install -y python-opencv
RUN echo 'ln /dev/null /dev/raw1394' >> ~/.bashrc
# RUN sudo ln /dev/null /dev/raw1394

#
# Install Tools
#
RUN sudo apt-get install -y git
