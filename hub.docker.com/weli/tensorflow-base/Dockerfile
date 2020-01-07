FROM ubuntu:18.04
RUN apt update
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt install apt-utils coreutils curl gnupg tzdata supervisor -qy
# config tzdata
RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

RUN echo "deb http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | \ 
    tee /etc/apt/sources.list.d/tensorflow-serving.list && \ 
    curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | apt-key add -

RUN apt update
RUN apt install python3 python3-pip python3-opencv tensorflow-model-server -qy

COPY models /root/models
WORKDIR /root/models/head-yolo
RUN cat * > model.h5
WORKDIR /root/models/openpose
RUN cat * > model.h5
WORKDIR /