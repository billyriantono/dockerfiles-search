FROM yantonov/anaconda3

MAINTAINER Yury Antonov <yantonov@yandex.ru>

# Downgrade to python 3.6
RUN /opt/conda/bin/conda install python=3.6.6

RUN /opt/conda/bin/conda config --add channels conda-forge

# install
RUN /opt/conda/bin/pip install --ignore-installed --upgrade \
     https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.13.1-cp36-cp36m-linux_x86_64.whl

ADD files/conda_requirements.txt /
RUN /opt/conda/bin/conda install -y --file /conda_requirements.txt
ADD files/requirements.txt /
RUN /opt/conda/bin/pip install -r /requirements.txt

RUN /opt/conda/bin/conda clean --packages

# data files for tensorboard
RUN mkdir -p /data

# required for opencv-python
RUN apt-get update && apt-get install -y \
    libsm6 \
    libxrender1 \
    libxext6 \
    libfontconfig1
