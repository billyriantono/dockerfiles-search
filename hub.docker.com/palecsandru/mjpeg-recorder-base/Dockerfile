FROM ubuntu:16.04

RUN mv /etc/localtime /etc/localtime.bak && ln -s /usr/share/zoneinfo/Europe/Bucharest /etc/localtime
RUN apt-get update
RUN apt-get install -y \
    ffmpeg \
    libsm6 \
    libxext6 \
    libxrender-dev \
    python3 \
    python3-pip

