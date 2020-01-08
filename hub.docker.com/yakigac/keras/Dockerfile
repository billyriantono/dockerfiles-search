FROM tensorflow/tensorflow:latest-gpu-py3
MAINTAINER Ryohei Kuroki <ryohei.kuroki@gmail.com>

RUN pip install -q keras
RUN pip install -q h5py

COPY jupyter_notebook_config.py /root/.jupyter/
