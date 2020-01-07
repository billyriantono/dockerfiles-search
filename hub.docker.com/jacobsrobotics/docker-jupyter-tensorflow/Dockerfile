FROM nvidia/cuda:8.0-devel

MAINTAINER Tobias Fromm <t.fromm@jacobs-university.de>

# Install git and iTorch dependencies
RUN apt-get update && apt-get install -y \
    sudo \
    python-pip \
    software-properties-common \
    git \
    wget \
    libzmq3-dev \
    libssl-dev \
    python-zmq

RUN pip install --upgrade pip

WORKDIR /root

# Install miniconda
ENV CONDA_DOWNLOAD_SCRIPT Miniconda3-latest-Linux-x86_64.sh
ENV CONDA_DIR /opt/conda

RUN wget -q https://repo.continuum.io/miniconda/$CONDA_DOWNLOAD_SCRIPT && \
    bash $CONDA_DOWNLOAD_SCRIPT -b -p $CONDA_DIR && \
    rm $CONDA_DOWNLOAD_SCRIPT

ENV PATH $CONDA_DIR/bin:$PATH

WORKDIR /root/dev

# update some packages
RUN conda update -n base conda

# create Anaconda environment
RUN conda create -n tensorflow pip python=3.6
RUN . /opt/conda/etc/profile.d/conda.sh
RUN ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh

# install matplotlib                                                                                                                                                                                                                   
RUN [ "/bin/bash", "-c", "source activate tensorflow && pip install matplotlib"]

# fix some weird error regarding an outdated dateutil version
RUN [ "/bin/bash", "-c", "source activate tensorflow && pip install python-dateutil --upgrade"]

# install tensorflow
RUN apt-get update && apt-get install -y \
	libcupti-dev \
	python3-pip
RUN [ "/bin/bash", "-c", "source activate tensorflow && pip install --upgrade pip" ]
#RUN [ "/bin/bash", "-c", "source activate tensorflow && pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.8.0-cp36-cp36m-linux_x86_64.whl" ]
RUN [ "/bin/bash", "-c", "source activate tensorflow && pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.4.1-cp36-cp36m-linux_x86_64.whl" ]

# use Anaconda environments inside Jupyter
RUN [ "/bin/bash", "-c", "source activate tensorflow && conda install numpy scipy pyyaml mkl mkl-include setuptools cmake cffi typing nb_conda jupyter"]

# Default command is to run the itorch-notebook
CMD ["/bin/bash", "-c", "source activate tensorflow && jupyter notebook --ip=0.0.0.0 --no-browser --allow-root"]
#CMD /bin/bash -c "tail -f /dev/null"
