FROM nvidia/cuda:10.0-cudnn7-devel   
# start with the nvidia container for cuda 10 with cudnn7

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install wget unzip lsof apt-utils lsb-core sudo -y
RUN apt-get install libatlas-base-dev -y
RUN apt-get install libopencv-dev python-opencv python-pip git-all -y   

RUN git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git --recurse-submodules

WORKDIR openpose
RUN cp -r ./scripts/ubuntu_deprecated/ ./scripts/ubuntu/
# RUN chmod -R +x ./scripts/ubuntu; sync; sleep 1; ./scripts/ubuntu/install_caffe_and_openpose_if_cuda8.sh
