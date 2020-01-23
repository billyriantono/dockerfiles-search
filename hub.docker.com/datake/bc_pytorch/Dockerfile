FROM pytorch/pytorch:0.4.1-cuda9-cudnn7-devel
ARG PYTHON_VERSION=3.6

RUN pip install --upgrade pip
RUN pip install pandas face-alignment &&\
    apt-get update -y &&\
    apt-get install -y python-opencv ffmpeg && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*
