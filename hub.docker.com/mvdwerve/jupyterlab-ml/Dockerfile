# base it on a normal miniconda3 install
FROM continuumio/miniconda3
MAINTAINER Michael van der Werve <mvdwerve@outlook.com>

# default packages
RUN conda install --yes \
	nodejs \
        matplotlib \
        opencv \
        pandas \
        scipy \
        scikit-learn \
        numpy \
        jupyterlab

# install torch
RUN conda install pytorch-cpu torchvision-cpu -c pytorch

# install the tensorboard extension
RUN pip install git+https://github.com/lanpa/tensorboard-pytorch

# jupyterlab point
EXPOSE 8888

# define that the normal directory is code
VOLUME ["/project"]
WORKDIR /project

# by default, start jupyterlab
CMD jupyter-lab --allow-root --ip=0.0.0.0 --no-browser --NotebookApp.token="" 
