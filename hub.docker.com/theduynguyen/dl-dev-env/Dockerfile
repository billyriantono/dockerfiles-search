FROM ubuntu:16.04

ARG conda_version=Miniconda2-4.3.11

# Conda
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH

RUN apt-get update && apt-get install -y bzip2 

RUN mkdir -p $CONDA_DIR && \
    echo export PATH=$CONDA_DIR/bin:'$PATH' > /etc/profile.d/conda.sh && \
    apt-get update && \
    apt-get install -y wget git libhdf5-dev g++ graphviz && \
    wget --quiet https://repo.continuum.io/miniconda/${conda_version}-Linux-x86_64.sh && \
    echo "d573980fe3b5cdf80485add2466463f5 *${conda_version}-Linux-x86_64.sh" | md5sum -c - && \
    /bin/bash /${conda_version}-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
    rm ${conda_version}-Linux-x86_64.sh

# Python env
RUN pip install ipdb pytest xmltodict pytest-cov python-coveralls coverage pytest-xdist pep8 pytest-pep8 pydot_ng jedi nose rednose Flask && \
    conda install Pillow scikit-image scikit-learn notebook pandas seaborn matplotlib pyyaml six h5py && \
    pip install tensorflow && \
    pip install keras && \
    conda clean -yt

# create directories /src, /data, /work for user and grant access to vimrc
ENV NB_USER deeplearner
ENV NB_UID 1000

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    chown -R deeplearner /home/deeplearner && \
    mkdir -p $CONDA_DIR && \
    mkdir -p /src && \
    mkdir -p /data && \
    mkdir -p /work && \
    chown deeplearner $CONDA_DIR -R && \
    chown deeplearner /src && \
    chown deeplearner /data && \
    chown deeplearner /work

USER deeplearner

# set current dir
ENV PYTHONPATH='/src/:$PYTHONPATH'
ENV PYTHONDONTWRITEBYTECODE=True
ENV TERM=xterm-256color
WORKDIR /src

#Ports
# Tensorboard
EXPOSE 6006
#Jupyter notebook
EXPOSE 8888

# Start Jupyter notebook (can be overriden)
CMD jupyter notebook --port=8888 --no-browser --ip=0.0.0.0
