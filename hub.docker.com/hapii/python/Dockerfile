FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade -y && apt-get install -y python3-pip python3-dev build-essential cmake git unzip pkg-config libopenblas-dev liblapack-dev libhdf5-serial-dev python3-h5py graphviz python3-opencv python3-scipy python3-matplotlib wget

RUN wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.243-1_amd64.deb && dpkg -i cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
RUN apt-get update && wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb && apt install -y ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
RUN apt-get update && apt-get install -y --no-install-recommends cuda-10-1 libcudnn7=7.6.4.38-1+cuda10.1 libcudnn7-dev=7.6.4.38-1+cuda10.1 libnvinfer6=6.0.1-1+cuda10.1 libnvinfer-dev=6.0.1-1+cuda10.1 libnvinfer-plugin6=6.0.1-1+cuda10.1

# RUN pip3 install -U virtualenv
# RUN virtualenv --system-site-packages -p python3 ./venv
#  && source ./venv/bin/activate
# RUN pip install --upgrade pip

COPY requirements.txt ./
# RUN pip install --no-cache-dir -r requirements.txt
RUN pip3 install --no-cache-dir -r requirements.txt
# docker build . -t 192.168.105.200:5000/python:3
# docker push 192.168.105.200:5000/python:3

# docker build . -t gcr.io/hapii-project/python:3
# docker push gcr.io/hapii-project/python:3

