FROM ubuntu:latest
MAINTAINER https://medium.com/@a29988122

# Add project source
WORKDIR /home
COPY . /home
ENV APP_ENV=docker

# Install dependencies
RUN apt-get update -y && apt-get install build-essential unzip -y
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:mc3man/bionic-media -y && add-apt-repository ppa:deadsnakes/ppa -y

RUN apt-get install git ffmpeg libopus-dev libffi-dev libsodium-dev python3.6 -y
RUN apt-get upgrade -y
RUN apt-get install curl -y
RUN apt-get install python3-distutils -y
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python3.6 get-pip.py

RUN python3.6 -m pip install -U pip
RUN python3.6 -m pip install -U -r requirements.txt 

ENTRYPOINT ["python3", "dockerentry.py"]