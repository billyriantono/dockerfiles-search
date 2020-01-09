FROM ubuntu:18.04

RUN apt update
RUN apt -y upgrade
RUN apt -y install wget cmake g++ clang git libtbb-dev vim

ENV HOME=/root
WORKDIR $HOME

CMD ["/bin/bash"]
