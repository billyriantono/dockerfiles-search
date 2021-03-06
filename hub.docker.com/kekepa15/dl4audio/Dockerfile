# FROM tensorflow/tensorflow:latest-gpu 
FROM tensorflow/tensorflow:1.10.0-gpu-py3

ENV LANG C.UTF-8

# pip libraries
RUN pip install --upgrade pip\
    && pip install virtualenv librosa fire tqdm glob3\
    && pip install --upgrade cython\
    && pip install madmom seaborn keras keras-vis spotipy


# Pytorch install
RUN pip install torch\
    && pip install torchvision


# Essentia install
RUN apt-get update && apt-get install -y python3-numpy python3-six \
    libfftw3-3 libyaml-0-2 libtag1v5 libsamplerate0 libavcodec-ffmpeg56 \
    libavformat-ffmpeg56 libavutil-ffmpeg54 \
    libavresample-ffmpeg2 python3-yaml

RUN apt-get update \
    && apt-get install -y build-essential python3-dev git \
    libfftw3-dev libavcodec-dev libavformat-dev libavresample-dev \
    libsamplerate0-dev libtag1-dev libyaml-dev \
    && mkdir /essentia && cd /essentia && git clone https://github.com/MTG/essentia.git \
    && cd /essentia/essentia && python3 waf configure --with-python \
    && python3 waf && python3 waf install && ldconfig \
    &&  apt-get remove -y build-essential libyaml-dev libfftw3-dev libavcodec-dev \
        libavformat-dev libavutil-dev libavresample-dev python-dev libsamplerate0-dev \
        libtag1-dev python-numpy-dev \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && cd / && rm -rf /essentia/essentia

RUN apt-get update \
    && apt-get install -y libav-tools \
    && apt-get install -y htop \
    && apt-get install -y vim


RUN apt-get update\
	&& pip install stempeg\
	&& pip install musdb\
	&& pip install museval


ENV PYTHONPATH /usr/local/lib/python3/dist-packages


WORKDIR /home
