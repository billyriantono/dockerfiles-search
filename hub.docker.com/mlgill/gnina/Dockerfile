FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
ARG GNINA_BASE_COMMIT=daf2689cfe0605113b6e0d099ca91f1b89734901
ARG GNINA_MODEL_COMMIT=27010c6e1cc8b17dbab1a189e767acc1f28424ef
ARG GNINA_SCRIPT_COMMIT=71915cb93002742f0503dff3cebf7d61e51b9c41

RUN apt-get update --fix-missing && \
    apt-get install -y build-essential \
                       git \
                       wget \
                       libopenbabel-dev \
                       libboost-all-dev \
                       libeigen3-dev \
                       libgoogle-glog-dev \
                       libprotobuf-dev \
                       protobuf-compiler \
                       libhdf5-serial-dev \
                       libatlas-base-dev \
                       python-dev \
                       cmake \
                       librdkit-dev \
                       python-numpy \
                       python-pip \
                       vim \
                       tmux && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*


ENV PYTHONPATH=/usr/local/python:$PYTHONPATH

RUN pip install --no-cache-dir matplotlib==2.2.3 \
                               scipy \
                               sklearn \
                               scikit-image \
                               protobuf \
                               psutil \
                               numpy \
                               seaborn \
                               ipython==5.0 \
                               ipykernel==4.10 \
                               jupyter \
                               notebook


# Gnina base directory
RUN git clone https://github.com/gnina/gnina.git /gnina && \
    cd /gnina && \
    git checkout ${GNINA_BASE_COMMIT} && \
    mkdir build && \
    cd build && \
    cmake -DCUDA_ARCH_NAME=All .. && \
    make && \
    make install

# Gnina models and scripts
RUN cd /gnina && \
    git clone https://github.com/gnina/models.git models && \
    cd /gnina/models && \
    git checkout ${GNINA_MODEL_COMMIT}

RUN cd /gnina && \
    git clone https://github.com/gnina/scripts.git scripts2 && \
    cd /gnina/scripts2 && \
    git checkout ${GNINA_SCRIPT_COMMIT}


# Add Jupyter configuration
RUN mkdir -p /root/.jupyter/nbconfig
COPY dockerfiles/jupyter_notebook_config.py /root/.jupyter/
COPY dockerfiles/edit.json /root/.jupyter/nbconfig/

COPY dockerfiles/wrapper.sh /.
RUN chmod 755 /wrapper.sh
ENV NBPASSWORD GNINA

ENV TERM xterm

RUN mkdir /data
WORKDIR /data
CMD /wrapper.sh



