# nikhilmetrani/tensorflow-cpu:latest + keras
# docker build -t nikhilmetrani/keras-tf-cpu:latest .

FROM nikhilmetrani/tensorflow-cpu:latest
MAINTAINER Nikhil Metrani <Nikhil Metrani>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --no-install-recommends \
            libhdf5-serial-dev \
            libhdf5-mpich-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir \
        pyyaml \
        h5py \
        image \
        seaborn \
        keras

COPY support/keras_getting_started.ipynb /home/
