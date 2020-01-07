FROM ubuntu:18.04

LABEL version="1.0" 
LABEL maintainer="Yogi Hardi <yogi.hardi@gmail.com>"

RUN apt-get update && apt-get install -y wget build-essential pkg-config make yasm

RUN mkdir /ffmpeg
WORKDIR /ffmpeg
RUN wget https://ffmpeg.org/releases/ffmpeg-4.2.1.tar.bz2
RUN tar -xvjf ffmpeg-4.2.1.tar.bz2
WORKDIR /ffmpeg/ffmpeg-4.2.1
RUN ./configure 
RUN make 
RUN make install
