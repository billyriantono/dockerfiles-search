FROM ubuntu:bionic
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install python3-dev python3-pip apt-utils wget -y && pip3 install pip --upgrade
RUN pip3 install cython pytest numpy pandas matplotlib jupyter zeep
RUN jupyter notebook --generate-config
RUN mkdir /input
WORKDIR /input