FROM ubuntu:18.04
LABEL maintainer=="Lukasz Laszko <lukaszlaszko@docker.com>"

# set environment variables
ENV DEBIAN_FRONTEND=noninteractive

# install tools and compilers
RUN apt-get -y update
RUN apt-get install -y xz-utils wget curl sudo
RUN apt-get install -y cmake ninja-build git-all doxygen
RUN apt-get install -y libboost-all-dev
RUN apt-get install -y clang lldb
RUN apt-get install -y g++ gdb
RUN apt-get install -y python-pip
RUN apt-get install -y python3-pip
RUN apt-get install -y libxerces-c-dev
RUN apt-get install -y pkg-config libcapstone-dev
