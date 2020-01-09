FROM ubuntu:16.10

maintainer info@markusqua.de

RUN apt-get update && apt-get install \
    ruby-dev \
    texlive-full \
    texlive-fonts-extra \
    -y

RUN apt-get install g++ make -y
RUN apt-get install rubber -y
RUN apt-get install git -y
RUN apt-get install python3 python3-pip -y
