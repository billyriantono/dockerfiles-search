FROM tensorflow/tensorflow:latest-gpu-py3
MAINTAINER Laurent Erignoux <lerignoux@gmail.com>

RUN pip install --upgrade pip
RUN pip install pysocks

RUN mkdir /srv/app
WORKDIR /srv/app

COPY ./requirements.txt .

RUN pip install -r requirements.txt
