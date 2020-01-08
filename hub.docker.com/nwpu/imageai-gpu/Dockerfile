FROM nvidia/cuda:10.1-cudnn7-devel

RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN apt update && apt install libopencv-dev python3 python3-pip -y
RUN pip3 install --upgrade pip setuptools virtualenv
RUN pip3 install tensorflow numpy scipy opencv-python pillow matplotlib h5py keras jsonpickle requests imageai
