FROM tensorflow/tensorflow:latest-gpu

MAINTAINER Haitao Chen <haidaocht@gmail.com>

RUN echo 'deb http://archive.ubuntu.com/ubuntu trusty multiverse' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y git vim 

RUN pip install quandl, keras, tflearn

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]