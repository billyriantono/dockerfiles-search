FROM python:2.7

RUN apt-get update && apt-get install -y \
    libblas-dev \
    liblapack-dev \
    gfortran \
    python-dev \
    python-numpy \
    python-scipy

RUN pip install numpy==1.9.3
RUN pip install scipy==0.16.0
RUN pip install talon==1.0.9
