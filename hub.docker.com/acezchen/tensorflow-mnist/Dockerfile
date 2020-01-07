FROM ubuntu:16.04
MAINTAINER Ace Chen 272716025@qq.com


#Install Python3.5

Run apt-get update && \
    apt-get install -y --no-install-recommends python3 && \
    apt-get install -y --no-install-recommends python3-matplotlib && \
    apt-get install -y --no-install-recommends python3-tk && \
    apt-get install -y --no-install-recommends python3-pip && \
    pip3 install --upgrade pip setuptools && \
    pip3 install --upgrade matplotlib && \


#Install TensorFlow CPU

    pip3 install --upgrade tensorflow


#Specify working folder

RUN mkdir /workspace
WORKDIR "/workspace"


#For Tensorboard
EXPOSE 6006


#Run shell

CMD ["/bin/bash"]
