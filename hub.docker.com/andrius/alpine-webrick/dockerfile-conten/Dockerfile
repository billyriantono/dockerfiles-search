FROM maven:3.6-jdk-8-slim

# install latest java
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get clean

# add user robot that can use sudo
RUN groupadd robot && useradd -ms /bin/bash robot -g robot && \
    apt-get install -y sudo && \
    #allow to use sudo by user robot
    echo "robot ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/robot && \
    chmod 0440 /etc/sudoers.d/robot

USER robot
WORKDIR /home/robot