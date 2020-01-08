FROM ubuntu:17.10

MAINTAINER Toshiaki Inahata <inahata@miharu.co.jp>


#
# Set UP Ubuntu
#
RUN apt-get update && apt-get upgrade -y && apt-get install -y git curl wget unzip vim

#
# Install Python
#
RUN apt-get install -y python3-pip python3-dev

RUN python3 --version
RUN pip3 --version

RUN pip3 install --upgrade pip

#
# Install Libraries
#
RUN pip3 install Pillow
RUN pip3 install --upgrade tensorflow==1.6.0

#
# Install OpenCV
#
RUN apt-get install -y python-opencv
RUN echo 'ln /dev/null /dev/raw1394' >> ~/.bashrc
