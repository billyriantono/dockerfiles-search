FROM ubuntu:trusty


MAINTAINER Konstantin Malanchev "hombit@gmail.com"


# Set locale to utf-8
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8


RUN apt-get -y update


# Python 3 with modules
RUN apt-get install --yes python3 python3-pip python3-requests ipython3
RUN pip3 install psutil
RUN pip3 install pika


# Install git
RUN apt-get install --yes git


# Clone repo
RUN git clone https://github.com/hombit/homger /app


# Create queue dir
RUN mkdir -p /var/local/app


WORKDIR /app/src
