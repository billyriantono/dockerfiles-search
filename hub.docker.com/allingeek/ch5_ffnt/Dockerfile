#FROM tensorflow/tensorflow:1.14.0-gpu-py3
FROM pytorch/pytorch:latest
MAINTAINER allentseng <allen050883@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive


RUN apt update -y;\
    apt install tzdata -y ;\

RUN apt update -y;\
    apt install git -y;\
    apt install vim -y;\
    apt install nano -y;\
    apt install -y libsm6 libxext6 -y;\
    apt-get install libxrender1 -y;\
    apt-get install libxext-dev -y

RUN pip install scipy;\
    pip install pandas;\
    pip install scikit-image;\
    pip install matplotlib;\
    pip install opencv-python

#RUN mkdir /workspace
#WORKDIR /workspace

# IPython
EXPOSE 8888
# TensorBoard
EXPOSE 6006


CMD ["bash"]
