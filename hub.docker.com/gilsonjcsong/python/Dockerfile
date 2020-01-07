FROM ubuntu:16.04

MAINTAINER gilson <chaijongsong@gmail.com>

# 환경변수 설정 (옵션)
ENV PATH /usr/local/bin:$PATH
ENV LANG C.UTF-8

# 기본 패키지들 설치 및 Python 3.6 설치
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:fkrull/deadsnakes
RUN apt-get update
RUN apt-get install -y --no-install-recommends python3.6 python3.6-dev python3-pip python3-setuptools python3-wheel gcc
RUN apt-get install -y git

# pip 업그레이드
RUN python3.6 -m pip install pip --upgrade


ADD . /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt .

RUN apt-get update && \
	apt-get install -y build-essential wget unzip bzip2 software-properties-common python-setuptools \
						pkg-config libboost-python-dev libboost-thread-dev libbluetooth-dev libglib2.0-dev \
						bluez bluez-hcidump libglib2.0-dev libasound-dev portaudio19-dev libportaudio2 libportaudiocpp0 ffmpeg libav-tools libavcodec-extra	

RUN ln -s /usr/lib/x86_64-linux-gnu/libboost_python-py35.so /usr/lib/x86_64-linux-gnu/libboost_python-py34.so 

RUN pip3 install -r requirements.txt 

CMD ["/bin/sh"]

