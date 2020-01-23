FROM ubuntu:14.04

RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    gfortran \
    git \
    libblas-dev \
    libffi-dev \
    liblapack-dev \
    libssl-dev \
    python-dev \
    python-pip

RUN pip install numpy
RUN pip install scipy
RUN pip install pandas
