FROM continuumio/miniconda3

RUN apt-get update

RUN apt-get install -y \
  gcc \
  libsm6 \
  libxext6 \
  libxrender-dev

RUN conda install -y \
  flask \
  opencv \
  pandas \
  scikit-image \
  tensorflow=1.14

RUN conda install -c pytorch -c fastai fastai
