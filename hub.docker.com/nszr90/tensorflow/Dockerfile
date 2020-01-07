FROM tensorflow/tensorflow:1.10.0-gpu-py3

LABEL maintainer "nszr90 <elvinchan@foxmail.com>"

RUN apt-get update && apt-get install -y \
    wget \
    zip \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
