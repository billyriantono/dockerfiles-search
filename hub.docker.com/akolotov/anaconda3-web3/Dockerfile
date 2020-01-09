FROM continuumio/anaconda3:latest

RUN apt-get -y install linux-headers-amd64 build-essential libssl-dev

RUN pip install web3 py_ecc ethereum

RUN /opt/conda/bin/conda install jupyter -y --quiet

WORKDIR /opt/notebooks

EXPOSE 8888

