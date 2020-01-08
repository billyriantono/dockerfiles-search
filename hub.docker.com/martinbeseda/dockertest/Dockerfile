FROM ubuntu:latest

RUN apt-get clean && apt-get update && apt-get install -y -V make cmake libboost-all-dev build-essential g++-8 git
RUN git clone https://github.com/ArashPartow/exprtk.git && cp exprtk/exprtk.hpp /usr/include
RUN git clone https://github.com/mat007/turtle.git 
RUN cp -r turtle/include/turtle /usr/include
