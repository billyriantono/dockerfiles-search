FROM ubuntu:18.04
MAINTAINER Minhyuk Kwon<minhyuk@suresofttech.com>

RUN apt-get update
RUN apt-get install -y python3
RUN apt-get install -y python3-pip
RUN pip3 install pyinstaller
RUN pip3 install requests
RUN pip3 install colorama
RUN pip3 install wcmatch
RUN pip3 install psutil
RUN pip3 install distro
RUN pip3 install hjson
RUN apt-get install -y cmake
RUN apt-get install -y git
RUN apt-get install -y dh-autoreconf
RUN apt-get install -y vim


CMD ["bash"]
