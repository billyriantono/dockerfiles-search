FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    build-essential \
    zlib1g \
    zlib1g-dev \
    git \
    python-qt4 \
    python-pyside \
    python-pip \
    python3-pip \
    python3-pyqt5 \
    make

RUN git clone https://github.com/jsh58/Genrich
WORKDIR "/Genrich"
RUN make



