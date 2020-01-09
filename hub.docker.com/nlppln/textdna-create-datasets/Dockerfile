FROM ubuntu:16.04

LABEL maintainer "j.vanderzwaan@esciencecenter.nl"

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
    build-essential \
    git \
    python2.7 \
    python2.7-dev \
    python-pip \
    && apt-get autoremove \
		&& apt-get clean

WORKDIR /code
RUN git clone https://github.com/jvdzwaan/Release-TextDNA.git && cd Release-TextDNA && git checkout dataset-docker

WORKDIR /code/Release-TextDNA
RUN pip install -e .

CMD /bin/bash
