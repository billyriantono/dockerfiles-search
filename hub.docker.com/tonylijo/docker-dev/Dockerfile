FROM ubuntu:16.04

MAINTAINER Tony Lijo Jose <mail@tonylijo.in> 

# update apt
RUN apt-get update

#in stall sudo package
RUN apt-get install -y sudo

# install git
RUN apt-get install -y git

# install vim
RUN apt-get install -y vim

# install build essential
RUN apt-get install -y build-essential

# install cmake 
RUN apt-get install -y cmake

# install python headers
RUN apt-get install -y python-dev python3-dev

# add username tony
RUN useradd -m -d /home/tony -G sudo tony -p poAjpfXvkMPIc

# default login directory
WORKDIR /home/tony 

# default user
USER tony

RUN git clone https://tonylijo@bitbucket.org/tonylijo/workspace_scripts.git ~/.tools

RUN cd .tools/ && ./install.sh
