FROM ubuntu:14.04
MAINTAINER Hariki Toshiki  <hariki@allegrosmart.com>

RUN apt-get update
RUN apt-get install -y git wget curl libgtk2.0-0

RUN git clone https://github.com/yyuu/pyenv.git ~/.pyenv

ENV PYENV_ROOT root/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc && \
    eval "$(pyenv init -)"

RUN pyenv install anaconda-2.4.0 && \
    pyenv global anaconda-2.4.0

RUN conda update conda
RUN conda install -c menpo opencv
RUN conda install tensorflow
RUN conda install keras
